<template>
  <div class="header">
    <div class="content-wrapper">
      <div class="avatar">
        <img :src="seller.avatar">
      </div>
      <div class="content">
        <div class="title">
          <span class="brand"></span>
          <span class="name">{{seller.name}}</span>
        </div>
        <div class="description">
          {{seller.description}} / {{seller.deliveryTime}}分钟送达
        </div>
        <div v-if="seller.supports" class="support">
          <span class="icon" :class="classMap[seller.supports[0].type]"></span>
          <span class="text">{{seller.supports[0].description}}</span>
        </div>
      </div>
      <div class="support-count" @click="showDetail">
        <span class="count">5个</span>
        <span class="icon-keyboard_arrow_right"></span>
      </div>
    </div>
    <div class="bulletin-content" @click="showDetail">
      <span class="bulletin"></span><span class="text">{{seller.bulletin}}</span>
      <span class="icon-keyboard_arrow_right"></span>
    </div>
    <div class="bg" :style="{'backgroundImage': 'url('+ seller.avatar +')'}"></div>
    <transition name="detail-fade">
    <div class="detail" v-show="detailShow">
      <div class="detail-content">
        <h1 class="name">{{seller.name}}</h1>
        <star :size="48" :score="seller.score"></star>
        <div class="line-title">
          <div class="liner"></div>
          <div class="text">优惠信息</div>
          <div class="liner"></div>
        </div>
        <ul class="supports">
          <li v-for="(support, $index) in seller.supports" :key="$index">
            <span class="icon" :class="classMap[support.type]"></span>
            <span class="description">{{support.description}}</span>
          </li>
        </ul>
        <div class="line-title">
          <div class="liner"></div>
          <div class="text">商家公告</div>
          <div class="liner"></div>
        </div>
        <p class="bulletin">{{seller.bulletin}}</p>
      </div>
      <div class="detail-close">
        <span class="icon-close" @click="hideDetail"></span>
      </div>
    </div>
    </transition>
  </div>
</template>

<script>
import star from '../star/star'

export default {
  props: {
    seller: {
      type: Object
    }
  },
  data: function () {
    return {
      detailShow: false
    }
  },
  created () {
    this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee']
  },
  methods: {
    // 打开商家详情
    showDetail () {
      this.detailShow = true
    },
    hideDetail () {
      this.detailShow = false
    }
  },
  components: {
    star
  }
}
</script>

<style lang="stylus">
@import "../../common/stylus/mixin.styl"
.header
  color: #fff
  background: rgba(0, 0, 0, 0.5)
  position: relative
  overflow: hidden
  .content-wrapper
    padding: 24px 12px 18px 24px
    font-size: 0
    position: relative
    .avatar
      width: 64px
      height: 64px
      display: inline-block
      vertical-align: top
      img
        width: 100%
        height: 100%
        -webkit-border-radius: 2px;
        -moz-border-radius: 2px;
        border-radius: 2px;
    .content
      display: inline-block
      margin-left: 16px
      vertical-align: top
      .title
        margin: 2px 0 8px 0
        .brand
          width: 30px
          height: 18px
          display: inline-block
          bg-image('images/brand')
          -webkit-background-size: 30px 18px
          background-size: 30px 18px
          vertical-align: middle
        .name
          font-size:16px
          font-weight: bold
          line-height: 18px
          margin-left:6px
          vertical-align: middle

      .description
        font-size: 12px
        line-height: 12px
      .support
        margin: 10px 0 2px 0
        .icon
          display: inline-block
          width: 12px
          height: 12px
          -webkit-background-size: 12px 12px
          background-size: 12px 12px
          vertical-align: top
          &.decrease
            bg-image('images/decrease_1')
          &.discount
            bg-image('images/discount_1')
          &.guarantee
            bg-image('images/guarantee_1')
          &.invoice
            bg-image('images/invoice_1')
          &.special
            bg-image('images/special_1')
        .text
          font-size: 10px
          vertical-align: top
          margin-left: 4px
    .support-count
      position: absolute
      width: 44px
      height: 24px
      line-height: 24px
      bottom: 15px
      right: 12px
      border-radius: 16px 14px 14px 16px
      background: rgba(0, 0, 0, 0.2)
      font-size: 0
      text-align: center
      .count
        font-size: 10px
      .icon-keyboard_arrow_right
        font-size: 10px
  .bulletin-content
    height: 28px
    line-height: 28px
    padding: 0 24px 0 12px
    background: rgba(7, 17, 27, 0.2)
    overflow: hidden
    white-space: nowrap
    text-overflow: ellipsis
    position: relative
    .bulletin
      width: 22px
      height: 12px
      display inline-block
      bg-image('images/bulletin')
      background-size: 22px 12px
      font-size: 10px
      vertical-align: top
      margin-top: 8px
    .text
      font-size: 10px
      vertical-align: top
      margin-left: 4px
    .icon-keyboard_arrow_right
      position: absolute
      right: 12px;
      line-height: 28px
  .bg
    position: absolute
    z-index: -1
    filter: blur(10px)
    width: 100%
    height: 100%
    top: 0
    left: 0
    overflow: hidden
  .detail
    position: fixed
    width: 100%
    height: 100%
    top: 0
    left: 0
    z-index: 1
    background: rgba(7, 17, 27, 0.7)
    overflow-y: auto
    .detail-content
      min-height: 100%
      width: 80%
      margin: 0 auto
      margin-bottom: -64px
      &:after
        content: ''
        display: block
        height: 64px
      .name
        font-size: 16px
        line-height: 16px
        font-weight: 700
        padding-top: 64px
        text-align: center
      .star
        margin: 16px auto 28px
        text-align: center
      .line-title
        display: flex
        margin: 0 auto 24px
        font-size: 0
        .liner
          flex: 1
          position: relative
          top: -7px
          border-bottom: 1px solid rgba(255, 255, 255, 0.2)
        .text
          font-size: 14px
          line-height: 14px
          font-weight: 700
          margin: 0 12px
      .supports
        padding: 0 12px 28px
        li
          font-size: 0
          margin-bottom: 12px
          .icon
            display: inline-block
            width: 16px
            height: 16px
            background-size: 16px 16px
            vertical-align: middle
            &.decrease
              bg-image('images/decrease_1')
            &.discount
              bg-image('images/discount_1')
            &.guarantee
              bg-image('images/guarantee_1')
            &.invoice
              bg-image('images/invoice_1')
            &.special
              bg-image('images/special_1')
          .description
            font-size: 12px
            line-height: 12px
            margin-left: 6px
            vertical-align: middle
      .bulletin
        padding: 0 12px
        font-size: 12px
        line-height: 24px
    .detail-close
      height: 64px
      text-align: center
      .icon-close
        font-size: 32px
        width: 32px
        height: 32px
        color: rgba(255, 255, 255, 0.5)
/* 可以设置不同的进入和离开动画 */
/* 设置持续时间和动画函数 */
.detail-fade-enter-active
  transition: all .3s ease;

.detail-fade-leave-active
  transition: all .8s cubic-bezier(1.0, 0.5, 0.8, 1.0);

.detail-fade-enter, .detail-fade-leave-to
  /* .slide-fade-leave-active for below version 2.1.8 */
  /* transform: translateX(10px); */
  opacity: 0;

</style>
