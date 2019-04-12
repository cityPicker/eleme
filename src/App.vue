<template>
  <div id="app">
    <v-header :seller="seller"></v-header>
    <div class="tab border-1px">
      <div class="tab-item">
        <router-link to="/goods">商品</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/ratings">评价</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/seller">商家</router-link>
      </div>
    </div>

    <router-view></router-view>
  </div>
</template>

<script>
import Header from './components/header/header'

const ERR_OK = 0
export default {
  name: 'App',
  data: function () {
    return {
      seller: {}
    }
  },
  components: {
    'v-header': Header
  },
  computed: {
    username () {
      return this.$route.params
    }
  },
  created () {
    // 获取header卖家信息
    this.$http.get('/api/seller').then(response => {
      response = response.body
      if (response.errno === ERR_OK) {
        this.seller = response.data
      }
    }, response => {
      console.log(response)
    })
  }
}
</script>

<style lang="stylus">
@import "common/stylus/mixin.styl"

.tab
  display: flex;
  display: -webkit-flex;
  text-align: center
  border-1px(rgb(7, 17, 27, 0.1))
  .tab-item
    flex: 1
    height: 40px;
    line-height: 40px;
    font-size: 14px
    color: rgb(77, 85, 93)
    a
      color: rgb(77, 85, 93)
      text-decoration: none;
      &.active
        color: rgb(240, 20, 20)
</style>
