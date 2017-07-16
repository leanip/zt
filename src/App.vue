<template>
  <div class="page">
    <v-header></v-header>

    <keep-alive>
      <router-view class="main"></router-view>
    </keep-alive>

    <footer class="footer border-top-1px">
      <div class="footer-item">
        <router-link to="/home"><span class="icon-home"></span></router-link>
      </div>
      <div class="footer-item">
        <router-link to="/category"><span class="icon-list"></span></router-link>
      </div>
      <div class="footer-item">
        <router-link to="/cart"><span class="icon-cart"></span></router-link>
      </div>
      <div class="footer-item">
        <router-link to="/user"><span class="icon-user"></span></router-link>
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
  position relative
  height 100%
  .main
    position fixed
    top 40px
    left 0
    bottom 40px
    width 100%
    overflow hidden
    z-index 0
  .footer
    display flex
    position fixed
    left 0
    bottom 0
    width 100%
    height: 40px
    line-height: 40px
    text-align center
    border-top-1px(rgba(7, 17, 27, 0.1))
    z-index 1
    .footer-item
      flex: 1
</style>
