<template>
  <div>
    <div v-if="info && deliviries">
      <h1 class="heading">Главная страница</h1>
      <img class="mainimage" :src="info.image" alt="" />
      <p class="main__text">{{ info.text }}</p>
      <h2>Все доставки</h2>
      <div v-for="(el, i) in del" :key="i" class="delivery">
        Доставка типа: {{ el.type }}
      </div>
    </div>
    <LoaderComponent v-else />
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
import LoaderComponent from '@/components/LoaderComponent.vue'
export default {
  name: 'IndexPage',
  components: { LoaderComponent },
  layout: 'DefaultLayout',
  data() {
    return {
      info: null,
      del: null,
    }
  },
  computed: {
    ...mapGetters({
      infoData: 'mainpage/getMainPage',
      deliviries: 'mainpage/getDel',
    }),
  },
  async mounted() {
    const data = await this.infoData
    this.info = data.data

    const dataa = await this.deliviries
    this.del = dataa.data
  },
}
</script>

<style>
.mainimage {
  display: block;
  max-width: 600px;
  margin: 0 auto;
  border-radius: 20px;
}
.main__text {
  padding: 20px;
}
.delivery {
  margin: 30px auto;
  text-align: center;
}
</style>
