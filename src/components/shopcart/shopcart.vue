<template>
  <div class="shop-cart">
    <div class="left-content">
      <div class="cart-icon">
        <div class="cart-inner" :class="{'highlight':totalCount}">
          <span class="icon-shopping_cart"></span>
        </div>
        <div class="count" v-show="totalCount">{{totalCount}}</div>
      </div>
      <span class="total-price" :class="{'highlight':totalPrice > 0}">￥{{totalPrice}}</span>
      <span class="delivery-price">另需配送费￥{{deliveryPrice}}元</span>
    </div>
    <div class="right-content" :class="payClass">{{payDesc}}</div>
  </div>
</template>

<script>
export default{
  props: {
    selectedFoods: {
      type: Array,
      default: function () {
        return [
          {
            price: 10,
            count: 2
          }
        ]
      }
    },
    deliveryPrice: {
      type: Number,
      default: 0
    },
    minPrice: {
      type: Number,
      default: 20
    }
  },
  computed: {
    totalPrice () {
      let totalPrice = 0
      this.selectedFoods.forEach((food) => {
        totalPrice += food.count * food.price
      })
      return totalPrice
    },
    totalCount () {
      let totalCount = 0
      this.selectedFoods.forEach((food) => {
        totalCount += food.count
      })
      return totalCount
    },
    payDesc () {
      if (this.totalPrice === 0) {
        return `￥${this.minPrice}起送`
      } else if (this.totalPrice < this.minPrice) {
        let diff = this.minPrice - this.totalPrice
        return `还差￥${diff}起送`
      } else {
        return `去结算`
      }
    },
    payClass () {
      if (this.totalPrice < this.minPrice) {
        return 'not-enough'
      } else {
        return 'enough'
      }
    }
  }
}
</script>

<style lang="stylus">
.shop-cart
  position: fixed
  display: flex
  width: 100%
  height: 48px
  bottom: 0
  left: 0
  background: #141d27
  .left-content
    position: relative
    flex: 1
    padding: 12px 12px 0 0
    .cart-icon
      position: absolute
      width: 56px
      height: 56px
      border-radius: 56px
      bottom: 2px
      left: 12px
      background: #141d27
      .cart-inner
        position: absolute
        width: 44px
        height: 44px
        border-radius: 44px
        bottom: 6px
        left: 6px
        background: rgba(255, 255, 255, 0.2)
        text-align: center
        &.highlight
          background: rgb(0, 160, 220)
          .icon-shopping_cart
            color: #fff
        .icon-shopping_cart
          font-size: 24px
          line-height: 44px
          color: rgba(255, 255, 255, 0.4)
      .count
        position: relative
        width: 24px
        height: 16px
        border-radius: 6px
        top: 0
        left: 34px
        background: rgb(240, 24, 24)
        box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.4)
        text-align: center
        line-height: 16px
        font-size: 9px
        color: #fff
        font-weight: 700
    .total-price
      padding: 0 12px 0 80px
      font-size: 16px
      color: rgba(255, 255, 255, 0.4)
      font-weight: 700
      line-height: 24px
      border-right: 1px solid rgba(255, 255, 255, 0.1)
      &.highlight
        color: #fff
    .delivery-price
      font-size: 10px
      color: rgba(255, 255, 255, 0.4)
      line-height: 24px
      padding-left: 12px
  .right-content
    flex: 0 0 105px
    width: 89px
    padding: 0 8px
    font-size: 12px
    font-weight: 700
    text-align: center
    line-height: 48px
    background: #2b333b
    color: rgba(255, 255, 255, 0.4)
    &.enough
      color: #fff
      background: #00b43c
</style>
