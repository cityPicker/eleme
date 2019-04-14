<template>
  <div class="controller">
    <div class="decrease icon-remove_circle_outline" v-show="food.count" @click="decreaseCart"></div>
    <div class="count" v-show="food.count">{{food.count}}</div>
    <div class="add icon-add_circle" @click="addCart"></div>
  </div>
</template>

<script>
import Vue from 'vue'

export default {
  props: {
    food: {
      type: Object
    }
  },
  methods: {
    addCart () {
      if (this.food.count) {
        this.food.count++
      } else {
        Vue.set(this.food, 'count', 1)
      }
    },
    decreaseCart () {
      if (this.food.count) {
        this.food.count--
      }
    }
  }
}
</script>

<style lang="stylus" scoped>
.controller
  font-size: 0
  .decrease, .add
    display: inline-block
    padding: 6px
    font-size: 24px
    color: rgb(0, 160, 220)
    line-height: 24px
    vertical-align: middle;
  .count
    display: inline-block
    font-size: 10px
    color: rgb(147, 153, 159)
    line-height: 24px
    vertical-align: middle;
</style>
