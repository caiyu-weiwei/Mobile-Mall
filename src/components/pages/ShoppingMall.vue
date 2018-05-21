<template>
  <div>
    <div class="search-bar">
      <van-row>
        <van-col span="3">
          <img :src="location" class="location-icon">
        </van-col>
        <van-col span="16">
          <input type="text" class="search-input">
        </van-col>
        <van-col span="5">
          <van-button size="mini">查询</van-button>
        </van-col>
      </van-row>
    </div>
    <div class="banner-area">
      <van-swipe :autoplay = "3000">
        <van-swipe-item v-for="(banner, index) in bannerArray" :key="index" v-lazy="banner">
          <img :src="banner.image" alt="banner">
        </van-swipe-item>
      </van-swipe>
    </div>
    <div class="nav-bar">
      <div v-for="(nav, index) in navList" :key="index">
        <img v-lazy="nav.image" style="width:90%;">
        <p>{{nav.mallCategoryName}}</p>
      </div>
    </div>
    <div class="adv-bar">
      <img v-lazy="advList.PICTURE_ADDRESS" style="width:100%;">
    </div>
    <div class="recommend-area">
      <div class="recommend-title">
        推荐商品
      </div>
      <div class="recommend-body">
        <swiper :options="swiperOption">
          <swiper-slide v-for="(item, index) in recommendGoods" :key="index" >
            <div class="recommend-item">
              <img :src="item.image" style="width:80%;">
              <div>{{item.goodsName}}</div>
              <div>￥{{item.price | moneyFilter}}(￥{{item.mallPrice | moneyFilter}})</div>
            </div>
          </swiper-slide>
        </swiper>
        <floorComponent :floorData="floor1" :floorName="floorName.floor1"></floorComponent>
        <floorComponent :floorData="floor2" :floorName="floorName.floor2"></floorComponent>
        <floorComponent :floorData="floor3" :floorName="floorName.floor3"></floorComponent>
        <div class="hot-area">
          <div class="hot-title">
            热销商品
          </div>
          <div class="hot-goods">
            <van-row>
              <van-col v-for="(item, index) in hotGoods" :key="index">
                <hotGoodsComponent :image="item.image" :goodsName="item.name" :goodsPrice="item.price" :mallPrice="item.mallPrice"></hotGoodsComponent>
              </van-col>
            </van-row>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import 'swiper/dist/css/swiper.css'
import { swiper, swiperSlide } from 'vue-awesome-swiper'
import floorComponent from '../component/floorComponent'
import { toMoney } from '@/filter/moneyFilter.js'
import hotGoodsComponent from '../component/hotGoodsComponent'
export default {
  data () {
    return {
      location: require('../../assets/images/location.png'),
      bannerArray: [],
      navList: [],
      advList: [],
      recommendGoods: [],
      swiperOption: {
        slidesPerView: 3
      },
      floor1: [],
      floor2: [],
      floor3: [],
      floorName: {},
      hotGoods: []
    }
  },
  components: {
    swiper,
    swiperSlide,
    floorComponent,
    hotGoodsComponent
  },
  created () {
    this.getDataList()
  },
  filters: {
    moneyFilter (money) {
      return toMoney(money)
    }
  },
  methods: {
    getDataList () {
      axios({
        url: 'https://www.easy-mock.com/mock/5ae424cfe3aaf3049f0674a3/index/',
        method: 'get'
      })
        .then((res) => {
          console.log(res)
          this.bannerArray = res.data.data.slides
          this.navList = res.data.data.category
          this.advList = res.data.data.advertesPicture
          this.recommendGoods = res.data.data.recommend
          this.floor1 = res.data.data.floor1
          this.floor2 = res.data.data.floor2
          this.floor3 = res.data.data.floor3
          this.floorName = res.data.data.floorName
          this.hotGoods = res.data.data.hotGoods
        })
        .catch((error) => {
          console.log(error)
        })
    }
  }
}
</script>

<style scoped>
.search-bar{
  height: 2.2rem;
  background-color: #e5017d;
  line-height: 2.2rem;
  overflow: hidden;
}
.location-icon{
  width: 80%;
  padding-top: .2rem;
  padding-left: .3rem;
}
.search-input{
  height: 1.4rem;
  border: 0;
  border-bottom: 1px solid #fff;
  background-color: #e5017d;
  color: #fff;
}
.banner-area{
  clear: both;
  max-height: 10rem;
}
.banner-area img{
  width: 100%;
}
.nav-bar{
  margin: .3rem;
  font-size: 14px;
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  background-color: #fff;
  border-radius: .3rem;
}
.nav-bar div{
  font-size: 12px;
  text-align: center;
  padding: .3rem;
}
.recommend-area{
  margin-top: .3rem;
  background-color: #fff;
}
.recommend-title{
  padding: .3rem;
  box-sizing: border-box;
  font-size: 14px;
  color: #FB0078;
  border: 1px solid #eee;
}
.recommend-item{
  border-right: 1px solid #eee;
  border-bottom: 1px solid #eee;
  font-size: 12px;
  text-align: center;
}
.hot-area{
  height: 1.8rem;
  line-height: 1.8rem;
  background-color: #fff;
  text-align: center;
  font-size: 14px;
}
.hot-goods{
  box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
</style>
