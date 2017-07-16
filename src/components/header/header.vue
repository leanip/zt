<template>
  <header class="header border-1px">
    <div class="logo-wrapper">
      <img class="logo" :src="logo" alt="">
    </div>
    <div class="search-wrapper">
      <div class="search">
        <span class="icon-search"></span>
      </div>
    </div>
  </header>
</template>
<script>
  export default{
    data() {
      return {
        logo: ''
      }
    },
    created: function(){
      let _this = this
      this.$ajax.get('/api/header')
        .then(function(res){
          _this.logo = res.data.data.logo
        })
        .catch(function(err){
          console.log(err)
        })
    }
  }
</script>
<style lang="stylus" rel="stylesheet/stylus">
@import '../../common/stylus/mixin.styl'
.header
  display flex
  position fixed
  top 0
  left 0
  width 100%
  height 40px
  line-height 40px
  border-1px(rgba(7, 17, 27, 0.1))
  .logo-wrapper
    flex: 1
    .logo
      width 80%
      margin-left 10%
  .search-wrapper
    flex 1
    .search
      float right
      width 60%
      height 30px
      margin-top 5px
      margin-right 10px
      border 1px solid #ccc
      border-radius 15px
      .icon-search
        float right
        display block
        margin 5px 5px 0 0
        font-size 20px
        color #ccc
</style>
