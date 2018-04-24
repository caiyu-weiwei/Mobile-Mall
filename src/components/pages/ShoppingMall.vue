<template>
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
</template>

<script>
export default {
  data () {
    return {
      location: require('../../assets/images/location.png')
    }
  }
}
</script>

<style scoped>
.search-bar{
  height: 2.2rem;
  background-color: #e5017d;
  line-height: 2.2rem;
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
</style>
