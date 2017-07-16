<template>
  <section ref="home">
    <div class="home-content">
      <div class="swiper-container carousel">
        <div class="swiper-wrapper">
          <div class="swiper-slide" v-for="(item, index) in carousels" :key="item.link">
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
      </div>
      <div class="home1">
        <div class="home-area1">
          <a :href="area1.link">
            <img :src="area1.img" alt="">
          </a>
        </div>
        <div class="home-area2">
          <a :href="area2.link">
            <img :src="area2.img" alt="">
          </a>
        </div>
      </div>
      <div class="home2">
        <a :href="area3.link">
          <img :src="area3.img" alt="">
        </a>
      </div>
      <div class="home3">
        <a :href="area4.link">
          <img :src="area4.img" alt="">
        </a>
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
      homeContent: {},
      carousels: [],
      area1: '',
      area2: '',
      area3: '',
      area4: ''
    }
  },
  created() {
    let _this = this
    this.$ajax.get('/api/home')
      .then(function(res){
        res = res.data
        _this.carousels = res.data.carousel
        _this.homeContent = res.data
        _this.area1 = res.data.area1
        _this.area2 = res.data.area2
        _this.area3 = res.data.area3
        _this.area4 = res.data.area4
        _this.$nextTick(()=>{
          _this._initScroll()
          _this._carousel()
        })
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
    },
    _carousel() {
      let mySwiper = new Swiper('.carousel', {
        direction: 'horizontal',
        loop: true,
        pagination: '.swiper-pagination',
        nextButton: '.swiper-button-next',
        prevButton: '.swiper-button-prev',
      })
    }
  }
}
</script>
<style lang="stylus" rel="stylesheet/stylus">
.home-content
  img
    width 100%
  .carousel
    font-size 0
    .swiper-pagination-bullet-active
      background #000
  .home1
    display flex
    margin-top 15px
    .home-area1
      flex 1
      margin-right 5px
    .home-area2
      flex 1
      margin-left 5px
</style>
