<template>
  <div class="header">
    <div class="header__logo">Деловая колбаса</div>
    <ul class="header__list">
      <li class="header__item"><a href="/">Главная</a></li>
      <li class="header__item"><a href="/about">Про нас</a></li>
      <li class="header__item"><a href="/add">Добавить</a></li>
    </ul>
    <div v-if="!widget">Загрузка</div>
    <div v-else class="widget">
      <div>trains:{{ widget.trains }}</div>
      <div>planes:{{ widget.trucks }}</div>
      <div>ships:{{ widget.trucks }}</div>
      <div>trucks:{{ widget.trucks }}</div>
    </div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
export default {
  name: 'HeaderComponent',
  data() {
    return {
      widget: null,
    }
  },
  computed: {
    ...mapGetters({
      infoData: 'mainpage/getWidget',
    }),
  },
  async mounted() {
    const data = await this.infoData
    this.widget = data.data
  },
}
</script>

<style scoped>
.header {
  width: 100%;
  display: flex;

  padding: 15px 10px;
}
.header__list {
  display: flex;
  flex-direction: row;
  list-style-type: none;
  gap: 10px;
}
.header__logo {
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 24px;
}
.header__item {
  padding: 7px 22px;
  border-radius: 8px;
  background: transparent;
}

.header__item a {
  color: #444444;
  text-decoration: none;
}

.widget {
  display: flex;

  gap: 10px;
}

.widget {
  scrollbar-width: thin;
  scrollbar-color: blue transparent;
}

/* Works on Chrome, Edge, and Safari */
.widget::-webkit-scrollbar {
  width: 1px;
}

.widget::-webkit-scrollbar-track {
  background: transparent;
}

.widget::-webkit-scrollbar-thumb {
  background-color: black;
  border-radius: 4px;
  width: 1px;
}
</style>
