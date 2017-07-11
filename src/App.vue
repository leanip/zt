<template>
  <div class="page">
    <v-header></v-header>
    
    <section class="main">
      <router-view></router-view>
    </section>

    <footer class="footer border-top-1px">
      <div class="footer-item">
        <router-link to="/home"><span class="">首页</span></router-link>
      </div>
      <div class="footer-item">
        <router-link to="/category"><span class="">分类</span></router-link>
      </div>
      <div class="footer-item">
        <router-link to="/cart"><span class="">购物车</span></router-link>
      </div>
      <div class="footer-item">
        <router-link to="/user"><span class="">我的</span></router-link>
      </div>
    </footer>
  </div>
</template>

<script>
import Header from 'components/header/header'
export default {
  name: 'app',
  components: {
    'v-header': Header
  }
}
</script>

<style lang="stylus" rel="stylesheet/stylus">
@import './common/stylus/mixin.styl'
.page
  display: flex
  height 100%
  flex-direction: column
  .main
    flex: 1
  .footer
    display: flex
    height: 40px
    line-height: 40px
    text-align center
    border-top-1px(rgba(7, 17, 27, 0.1))
    background #f90
    .footer-item
      flex: 1
      // text-indent -999px
</style>
