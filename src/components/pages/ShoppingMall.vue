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
              <div>￥{{item.price}}(￥{{item.mallPrice}})</div>
            </div>
          </swiper-slide>
        </swiper>
        <div class="floor-anormaly">
          <div class="floor-one">
            <img :src="floor1_0.image" style="width:100%;">
          </div>
          <div class="floor-two">
            <div>
            <img :src="floor1_1.image" style="width:100%;">
          </div>
          <div>
            <img :src="floor1_2.image" style="width:100%;">
          </div>
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
      floor1_0: {},
      floor1_1: {},
      floor1_2: {}
    }
  },
  components: {
    swiper,
    swiperSlide
  },
  created () {
    this.getDataList()
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
          this.floor1_0 = this.floor1[0]
          this.floor1_1 = this.floor1[1]
          this.floor1_2 = this.floor1[2]
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
  font-size: 12px;
  text-align: center;
}
.floor-anormaly{
  display: flex;
  flex-direction: row;
  background-color: #fff;
}
</style>
