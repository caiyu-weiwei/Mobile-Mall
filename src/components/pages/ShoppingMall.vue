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
          <img :src="banner.imageUrl" alt="banner">
        </van-swipe-item>
      </van-swipe>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      location: require('../../assets/images/location.png'),
      bannerArray: [
        {imageUrl: 'http://7xjyw1.com1.z0.glb.clouddn.com/simleVueDemoPic001.jpg'},
        {imageUrl: 'http://7xjyw1.com1.z0.glb.clouddn.com/simleVueDemoPic002.jpg'},
        {imageUrl: 'http://7xjyw1.com1.z0.glb.clouddn.com/simleVueDemoPic003.jpg'}
      ]
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
</style>
