<template>
  <div id="app">
    <v-header :seller="seller"></v-header>
    <div class="tab border-1px">
      <div class="tab-item">
        <router-link to="/goods">商品522222</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/ratings">评论222222</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/seller">商家</router-link>
      </div>
    </div>
    <router-view :seller="seller"></router-view>
  </div>
</template>

<script>
import header from '@/components/header/header'
const ERR_OK = 0
export default {
  data() {
    return {
      seller: {}
    }
  },
  created() {
    this.$http.get('/api/seller').then(response => {
      response = response.body
      if (response.errno === ERR_OK) {
        this.seller = response.data
      }
    })
  },
  components: {
    'v-header': header
  }
}
</script>

<style lang="stylus">
@import "./common/stylus/index"
  .tab
    display: flex
    width: 100%
    height: 40px
    line-height: 40px
    border-1px(#ddd)
    .tab-item
      flex: 1
      text-align: center
      & > a
        display: block
        font-size: 14px
        color: rgb(77,85,93)
        &.router-link-active
          color: rgb(240,20,20)
</style>
