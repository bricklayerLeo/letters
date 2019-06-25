<template>

  <div class="alphabet-container">
    <ul>
      <li v-for="(item,index) in letters" :key="item" @click="cityFilter(index,item)"
      @touchstart="touchStart" @touchmove="touchMove"
      @touchend="touchEnd" :ref="item"
     :class="{'current': currentIndex == index}"
      
      >{{ item }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  props: ['cities'],
  data() {
    return {
      touchStatus: false,
      timer: null,
      startY: 0,
      currentIndex:0
    }
  },
  computed: {
    letters(){
      let letters = []
      for(let i in this.cities){
        letters.push(i)
      }
      return letters
    }
  },
  updated() {
    
    this.startY = this.$refs['A'][0].offsetTop
  },
  methods: {
    cityFilter(index,item){
      this.$emit('cityFilter', item);
      console.log(item)
      this.currentIndex = index;
    },
    touchStart(){
      this.touchStatus = true
    },
    touchMove(e){
      if(this.touchStatus){
       
       
          const touchY =e.touches[0].clientY - 158
          const index = Math.floor((touchY - this.startY) / 20)

          if(index >= 0 && index < this.letters.length){
            this.$emit('cityFilter', this.letters[index])
            this.currentIndex = index
          }
      
      }
    },
    touchEnd(){
      this.touchStatus = false
    }
  },
  components: {

  }
}
</script>

<style scoped lang="scss">
.alphabet-container{
  width: .1rem;
  position: absolute;
  right: .3rem;
  top: 3rem;
  ul>li{
    width: .4rem;
    line-height: .4rem;
    color: #00bcd4;
    text-align: center;
    &.current{color: red}
        
  }
}
</style>
