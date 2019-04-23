<template>
  <div class="goods">
    <div class="menu-wrapper">
      <ul class="goods-menu">
        <li class="menu-item" v-for="(menuItem, $index) in goods" :key="$index">
          <span class="table-cell border-1px">
            <span v-show="menuItem.type>0" class="icon" :class="classMap[menuItem.type]"></span>
            <span class="name">{{menuItem.name}}</span>
          </span>
        </li>
      </ul>
    </div>
    <div class="foods-wrapper">
      <ul>
        <li class="foods-list-hock" v-for="(foods, $index) in goods" :key="$index">
          <h1 class="title">{{foods.name}}</h1>
          <ul class="food-list">
            <li class="food-item border-1px" v-for="(foodItem, $index) in foods.foods" :key="$index">
              <div class="pic">
                <img width="57px" height="57px" :src="foodItem.image">
              </div>
              <div class="content">
                <h1 class="name">{{foodItem.name}}</h1>
                <p v-if="foodItem.description" class="description">{{foodItem.description}}</p>
                <p class="ratings-item">
                  <span class="sell-count">月售{{foodItem.sellCount}}份</span>
                  <span class="rating">好评率{{foodItem.rating}}%</span>
                </p>
                <p class="price-item">
                  <span class="symbol">￥</span>
                  <span class="price">{{foodItem.price}}</span>
                  <span v-if="foodItem.oldPrice" class="old-price">￥{{foodItem.oldPrice}}</span>
                </p>
              </div>
              <div class="cart-control">
                <count-ctrl :food="foodItem"></count-ctrl>
              </div>
            </li>
          </ul>
        </li>
      </ul>
    </div>
    <shop-cart></shop-cart>
  </div>
</template>
<script>
import ShopCart from '../shopcart/shopcart'
import countController from '../coutController/coutController'

export default {
  data: function () {
    return {
      goods: {},
      foodsListHeight: []
    }
  },
  created: function () {
    // 商品数据
    this.$http.get('api/goods').then((response) => {
      response = response.body
      if (response.errno === 0) {
        this.goods = response.data
        this.$nextTick(
          // 计算右侧栏目高度
          this._calculateHeight()
        )
      }
    })
    // 促销类型类名
    this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee']
  },
  components: {
    'shop-cart': ShopCart,
    'count-ctrl': countController
  },
  methods: {
    _calculateHeight () {
      // 页面title高度数组
      //  滚动时候判断滚动的高度对应左侧导航
      //  优化：防抖动复用
      let foodsList = document.getElementsByClassName('foods-list-hock')
      foodsList = [...foodsList]
      console.log(foodsList instanceof Array)
      foodsList.forEach((item) => {
        alert(item)
      })
      alert(1)
    }
  }
}
</script>
<style lang="stylus">
@import '../../common/stylus/mixin.styl'
.goods
  display: flex
  position: absolute
  top: 174px
  bottom: 48px
  overflow: hidden
  .menu-wrapper
    flex: 0 0 80px
    width: 80px
    background: #f3f5f7
    overflow: hidden
    overflow-y: scroll
    .goods-menu
      width: 100%
      .menu-item
        display: table
        width: 56px
        height: 54px
        padding: 0 12px
        font-size: 0
        .table-cell
          display: table-cell
          vertical-align middle
          border-1px(rgba(7, 17, 27, 0.1))
          .icon
            display: inline-block
            width: 12px
            height: 12px
            -webkit-background-size: 12px 12px
            background-size: 12px 12px
            vertical-align: middle
            margin-right: 2px
            &.decrease
              bg-image('images/decrease_3')
            &.discount
              bg-image('images/discount_3')
            &.guarantee
              bg-image('images/guarantee_3')
            &.invoice
              bg-image('images/invoice_3')
            &.special
              bg-image('images/special_3')
          .name
            font-size: 12px
            line-height: 14px
            color: #07111b
            vertical-align: middle
        &.active
          background: #fff
          font-weight: 700
  .foods-wrapper
    flex: 1
    overflow: hidden
    overflow-y: scroll
    .title
      height: 26px
      padding-left: 14px
      line-height: 26px
      font-size: 12px
      color: rgb(147, 153, 159)
      background: #f3f5f7
      border-left: 2px solid #d9dde1
    .food-list
      padding: 0 18px
      .food-item
        display: flex
        padding: 18px 0
        border-1px(rgba(7, 17, 27, 0.1))
        &:last-child
          border-none()
        .pic
          flex: 0 0 57px
          width: 57px
          img
            border-radius: 2px
        .content
          flex: 1
          margin-left: 10px
          .name
            margin-top: 2px
            font-size: 14px
            line-height: 14px
            color: rgb(7, 17, 27)
            margin-bottom: 8px
          .description
            font-size: 10px
            line-height: 10px
            color: rgb(147, 153, 159)
            margin-bottom: 8px
          .ratings-item
            font-size: 0
            color: rgb(147, 153, 159)
            line-height: 10px
            .sell-count
              font-size: 10px
              margin-right: 12px
            .rating
              font-size: 10px
          .price-item
            font-size: 0
            .symbol
              font-size: 10px
              color: #f01414
            .price
              font-size: 14px
              color: #f01414
              font-weight: 700
              line-height: 24px
            .old-price
              font-size: 10px
              color: rgb(147, 153, 159)
              font-weight: 700
              line-height: 24px
              margin-left: 8px
              text-decoration: line-through
        .cart-control
          position: absolute
          bottom: 12px
          right: -6px
</style>
