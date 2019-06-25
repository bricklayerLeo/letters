<template>
  <div class="container" ref="wrapper">
    <div>
      <div class="my-city">
        <p class="city-title border-bottom">当前城市</p>
        <div class="button-wrap border-bottom">
          <span class="active-city"> 北京 </span>
        </div>
      </div>

      <div class="hot-cities">
        <p class="city-title border-bottom">热门城市</p>
        <div class="button-wrap border-bottom">
          <span @click="changeCity" v-for="item in hotCities" 
          :key="item.id">{{ item.name }}</span>
        </div>
      </div>

      <div class="all-cities">
        <div :ref="name" v-for="(value, name) in cities" :key="name"  class="cities-wrap">
          <p class="city-title border-bottom" ref="zimu">{{ name }}</p>
          <ul v-for="item in value" :key="item.id">
            <li @click="changeCity" 
            class="city-list border-bottom">{{ item.name }}</li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

import Bscroll from 'better-scroll'
export default {
  props: ['hotCities', 'cities', 'cityCap'],
  data() {
    return {
    }
  },
  methods: {
    changeCity(e){
      let cityName = e.target.innerText
      this.$store.commit('changeCity', cityName)
      this.$router.push('/')
    }
  },
  components: {

  },
  mounted () {
      this.scroll = new Bscroll(this.$refs.wrapper,{
          click: true
      })
  },
  watch: {
    gundong(){
      let zimu = this.$refs.zimu[0]
      if(zimu.offsetTop<200){
        zimu.style.position='fixed';
        zimu.style.top=0;
      }
    },
    cityCap(){
      let element = this.$refs[this.cityCap][0]
      this.scroll.scrollToElement(element)
    }
  },
  computed: {
     
  }
}
</script>

<style scoped lang="scss">
.container{
  //color: #666;
  overflow: hidden;
  position: absolute;
  top: 1.58rem;
  left: 0;
  right: 0;
  bottom: 0;
}
.city-title{
  line-height: .54rem;
  padding-left: .2rem;
  background-color: #eee;
}
.button-wrap{
  padding: .1rem .6rem .1rem .1rem;
  box-sizing: border-box;
  span{
    display: inline-block;
    border-radius: .06rem;
    width: 1.95rem;
    line-height: .5rem;
    border: .02rem solid #ccc;
    text-align: center;
    margin: .1rem;
  }
}
.city-list{
  padding: .2rem;
  line-height: .37rem;
}
.button-wrap .active-city{
  border: .02rem solid #00bcd4;
  color: #00bcd4;
}
</style>
