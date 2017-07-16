<template>
  <section ref="home">
    <div class="home-content">
      <div class="swiper-container carousel">
        <div class="swiper-wrapper">
          <div class="swiper-slide carousel-item" v-for="(item, index) in carousels">
            <a :href="item.link">
              <img class="carousel-img" :src="item.img" alt="">
            </a>
          </div>
        </div>
        <!-- 如果需要分页器 -->
        <div class="swiper-pagination"></div>
        <!-- 如果需要导航按钮 -->
        <div class="swiper-button-prev"></div>
        <div class="swiper-button-next"></div>
        <!-- 如果需要滚动条 -->
        <div class="swiper-scrollbar"></div>
      </div>
    </div>
  </section>
</template>
<script>
import BScroll from 'better-scroll'
import Swiper from 'static/js/swiper.min.js'
export default{
  data() {
    return {
      carousels: []
    }
  },
  created() {
    let _this = this
    this.$ajax.get('/api/home')
      .then(function(res){
        res = res.data
        _this.carousels = res.data.carousel
        _this.$nextTick(()=>{
          _this._initScroll()
        })
      })
  },
  mounted() {
    let mySwiper = new Swiper('.swiper-container', {
      direction: 'horizontal',
      loop: true,
      pagination: '.swiper-pagination',
      nextButton: '.swiper-button-next',
      prevButton: '.swiper-button-prev'
     })
  },
  methods: {
    _initScroll(){
      if(!this.scroll){
        this.scroll = new BScroll(this.$refs.home, {
          click: true,
          startX: 0,
          startY: 0
        })
      } else {
        this.scroll.refresh()
      }
    }
  }
}
</script>
<style lang="stylus" rel="stylesheet/stylus">
.carousel
  .carousel-item
    .carousel-img
      width 100%
</style>
