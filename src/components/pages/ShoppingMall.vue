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
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data () {
    return {
      location: require('../../assets/images/location.png'),
      bannerArray: [],
      navList: [],
      advList: []
    }
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
</style>
