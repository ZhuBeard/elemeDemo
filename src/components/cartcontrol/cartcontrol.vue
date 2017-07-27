<template>
  <div class="cartcontrol">
    <transition name="move">
      <div class="cart-decrease" v-show="food.count>0" @click="decreaseCart">
        <span class="inner">-</span>
      </div>
    </transition>
    <div class="cart-count" v-show="food.count>0">{{ food.count }}</div>
    <div class="cart-add" @click="addCart">+</div>
  </div>
</template>

<script>
import Vue from 'vue'
export default {
  props: {
    food: Object
  },
  methods: {
    addCart() {
      if (!this.food.count) {
        Vue.set(this.food, 'count', 1)
      } else {
        this.food.count++
      }
      this.$emit('cart.add', event.target)
    },
    decreaseCart() {
      if (this.food.count) {
        this.food.count--
      }
    }
  }
}
</script>

<style lang="stylus">
  .cartcontrol
    font-size: 0
    .cart-decrease
      display: inline-block
      transition: all .4s linear
      &.move-transition
        opacity: 1
        transform: translate3D(0,0,0)
      .inner
        display: block
        padding: 1px 5px 3px
        font-size: 16px
        line-height: 15px
        border:1px solid rgb(0,160,220)
        border-radius: 50%
        color: rgb(0,160,220)
      &.move-enter-active,&.move-leave-active
        opacity: 0
        transform: translate3D(24px,0,0)
    .cart-count
      display: inline-block
      vertical-align: top
      width: 24px
      line-height: 20px
      text-align: center
      font-size: 12px
      color: rgb(147,153,159)
    .cart-add
      display: inline-block
      padding: 1px 5px 3px
      font-size: 16px
      line-height: 15px
      background:rgb(0,160,220)
      border:1px solid rgb(0,160,220)
      border-radius: 50%
      color: #fff
</style>
