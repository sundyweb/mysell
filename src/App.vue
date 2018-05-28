<template>
  <div id="app">
   <v-header :seller ='seller'></v-header>
   <!-- 传递数据 -->
   <div class="tab border-1px">
     <div class="tab-item"><router-link to='goods'>商品</router-link></div>
     <div class="tab-item"><router-link to='ratings'>评价</router-link></div>
     <div class="tab-item"><router-link to='seller'>商家</router-link></div>
   </div>
   <keep-alive>
     <router-view :seller = "seller"></router-view>
   </keep-alive>
  </div>
</template>

<script>
// 引入组件
import header from './components/header'
import goods from './components/goods'
// 获取数据
import axios from 'axios'

export default {
  name: 'App',
  data () {
    return {
      seller: {}
    }
  },
  // 注册组件
  components: {
    'v-header': header,
    goods
  },
  // 获取数据
  created () {
    axios.get('/good/seller').then(res => {
      if (res.data.code === 0) {
        this.seller = res.data.data
        console.log(res)
      }
    })
  }
}
</script>

<style lang = 'stylus' ref = 'stylesheet/stylus'>
@import 'assets/stylus/index.styl'
#app
 .tab
  display flex
  height 40px
  line-height 40px
  border-1px(rgba(240,20,20,0.1))
  .tab-item
    flex 1
    text-align center
    font-size 14px
    color rgb(77,85,93)
    &.a
      width 100%
      height 100%
      display block
    a.active
      color rbg(240,20,20) !important;
</style>
