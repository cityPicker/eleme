<template>
  <div class="shop-cart">
    <div class="left-content">
      <div class="cart-icon">
        <div class="cart-inner">
          <span class="icon-shopping_cart"></span>
        </div>
      </div>
    </div>
    <div class="right-content"></div>
  </div>
</template>

<script>
export default{

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
    padding: 24px
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
        background: rgba(0, 0, 0, 0.2)
        text-align: center
        line-height: 44px
        .icon-shopping_cart
          font-size: 24px
          color: rgba(255, 255, 255, 0.4)
  .right-content
    flex: 0 0 105px
    width: 105px
</style>
