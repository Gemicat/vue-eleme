<template>
  <div class="cartControl">
    <transition name="fade">
      <div class="cart-decrease" v-show="food.count > 0" @click.stop.prevent="decreaseCart($event)">
        <transition name="inner">
          <span class="inner iconfont icon-jian"></span>
        </transition>
      </div>
    </transition>
    <span class="cart-count" v-show="food.count > 0">{{food.count}}</span>
    <span class="iconfont icon-jia cart-add" @click.stop.prevent="addCart($event)"></span>
  </div>
</template>

<script>
import Vue from 'vue';

export default {
  props: {
    food: {
      type: Object,
    },
  },
  methods: {
    addCart(event) {
      if (!event._constructed) {
        // 去掉自带click事件的点击
        return;
      }
      if (!this.food.count) {
        Vue.set(this.food, 'count', 1);
      } else {
        this.food.count += 1;
      }
      this.$emit('increment', event.target);
    },
    decreaseCart(event) {
      if (!event._constructed) {
        // 去掉自带click事件的点击
        return;
      }
      this.food.count -= 1;
    },
  },
};
</script>

<style lang="stylus" scoped>
@import 'cartControl.styl';
</style>


