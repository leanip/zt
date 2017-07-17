<template>
  <section ref="home">
    <div class="home-content">
      <div class="carousel-wrapper">
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
      <div class="celebrity">
        <div class="title">
          <div class="en">celebrity</div>
          <div class="cn">星闻速递</div>
        </div>
        <div class="list-wrapper">
          <div class="list">
            <div class="list-content">
              <div v-for="item in celebrity" :key="item.link" class="item">
                <a :href="item.link">
                  <img :src="item.img" alt="">
                </a>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="hotsale-title">
        <div class="en">hotsale</div>
        <div class="cn">最热单品</div>
      </div>
      <div class="hotsale-wrapper">
        <div class="swiper-container hotsale">
          <div class="swiper-wrapper">
            <div class="swiper-slide" v-for="(item, index) in hotsale" :key="item.link">
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
        carousels: [],
        area1: '',
        area2: '',
        area3: '',
        area4: '',
        celebrity: [],
        hotsale: []
      }
    },
    created() {
      let _this = this
      this.$ajax.get('/api/home')
        .then(function(res){
          res = res.data
          _this.carousels = res.data.carousel
          _this.area1 = res.data.area1
          _this.area2 = res.data.area2
          _this.area3 = res.data.area3
          _this.area4 = res.data.area4
          _this.celebrity = res.data.celebrity
          _this.hotsale = res.data.hotsale
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
            click: true
          })
        } else {
          this.scroll.refresh()
        }
      },
      _carousel() {
        let carouselSwiper = new Swiper('.carousel', {
          direction: 'horizontal',
          loop: true,
          autoplay: 3000,
          pagination: '.swiper-pagination',
          nextButton: '.swiper-button-next',
          prevButton: '.swiper-button-prev',
        })
        let hotsaleSwiper = new Swiper('.hotsale', {
          direction: 'horizontal',
          loop: true,
          autoplay: 3000,
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
  font-size 0
  .carousel-wrapper
    position relative
    width 100%
    height 0
    padding-top 88.27%
    .carousel
      position absolute
      top 0
      left 0
      width 100%
      height 100%
      .swiper-pagination-bullet-active
        background #000
  .home1
    position relative
    width 100%
    height 0
    margin-top 15px
    padding-top 55.2%
    .home-area1, .home-area2
      position absolute
      top 0
      width 50%
      height 100%
    .home-area1
      left 0
      padding-right 5px
    .home-area2
      right 0
      padding-left 5px
  .home2, .home3
    position relative
    width 100%
    height 0
    margin-top 15px
    padding-top 64.48%
    img
      position absolute
      top 0
      left 0
      width 100%
      height 100%
  .celebrity
    margin-top 15px
    .title
      text-align center
      letter-spacing 3px
      .en
        line-height 24px
        font-size 18px
        text-transform uppercase
      .cn
        margin-bottom 5px
        line-height 20px
        font-size 14px
    .list-wrapper
      position relative
      width 100%
      height 0
      padding-top 64.26%
      .list
        position absolute
        top 0
        left 0
        width 100%
        height 100%
        .list-content
          display flex
          margin 0 -5px
          .item
            flex 1
            padding 0 5px
  .hotsale-title
    margin-top 15px
    text-align center
    letter-spacing 3px
    .en
      line-height 24px
      font-size 18px
      text-transform uppercase
    .cn
      margin-bottom 5px
      line-height 20px
      font-size 14px
  .hotsale-wrapper
    position relative
    width 100%
    height 0
    padding-top 140.2%
    .hotsale
      position absolute
      top 0
      left 0
      width 100%
      height 100%
      .swiper-pagination-bullet-active
        background #000
</style>
