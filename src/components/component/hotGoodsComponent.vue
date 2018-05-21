<template>
  <div>
    <div class="hot-goods">
      <div>
        <img :src="image" style="width: 90%;">
      </div>
      <div class="goods-name">{{goodsName}}</div>
      <div class="goods-price">￥{{goodsPrice | moneyFilter}}(￥{{mallPrice | moneyFilter}})</div>
    </div>
  </div>
</template>
<script>
import { toMoney } from '@/filter/moneyFilter.js'
export default {
  props: ['image', 'goodsName', 'goodsPrice', 'mallPrice'],
  data () {
    return {}
  },
  filters: {
    moneyFilter (money) {
      return toMoney(money)
    }
  }
}
</script>
<style scoped>
.hot-goods{
  width: 10rem;
  background-color: #fff;
  font-size: 12px;
  border-top: 1px solid #eee;
  border-right: 1px solid #eee;
  box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
.goods-name{
  font-size: 12px;
}
</style>
