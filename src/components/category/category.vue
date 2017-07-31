<template>
  <section class="main">
    <div class="filter">
      <div class="filter-btn">
        <div class="classify">条件筛选</div>
        <div v-if="rank" class="rank">{{rank.current.title}}</div>
      </div>
    </div>
  </section>
</template>
<script>
  export default{
    data() {
      return {
        category: null,
        filter: null,
        rank: null
      }
    },
    created() {
      let _this = this
      this.$ajax.get('/api/category')
        .then(res => {
          res = res.data.data
          _this.category = res
          _this.filter = res.filter
          _this.rank = res.rank
          console.log(res.rank)
        })
    }
  }
</script>
<style>

</style>
