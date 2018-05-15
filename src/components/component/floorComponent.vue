<template>
  <div class="floor">
    <div class="floor-title">
      {{floorName}}
    </div>
    <div class="floor-anomaly">
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
    <div class="floor-nomaly">
      <div v-for="(item, index) in floorData.slice(3)" :key="index">
        <img :src="item.image" style="width: 100%;">
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      floor1_0: {},
      floor1_1: {},
      floor1_2: {}
    }
  },
  props: ['floorData', 'floorName'],
  watch: {
    floorData: {
      handler (val, oldVal) {
        if (val) {
          this.floor1_0 = val[0]
          this.floor1_1 = val[1]
          this.floor1_2 = val[2]
        }
      },
      deep: true
    }
  }
}
</script>

<style scoped>
.floor-title{
  height: 1.8rem;
  line-height: 1.8rem;
  font-size: 14px;
  text-align: center;
}
.floor-anomaly{
  display: flex;
  flex-direction: row;
  background-color: #fff;
  border-top: 1px solid #eee;
}
.floor-one{
  border-right: 1px solid #eee;
  border-bottom: 1px solid #eee;
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
}
.floor-two div{
  border-bottom: 1px solid #eee;
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
}
.floor-nomaly{
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}
.floor-nomaly div{
  width: 10rem;
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
  background-color: #fff;
  border-bottom: 1px solid #eee;
}
.floor-nomaly div:nth-child(odd){
  border-right: 1px solid #eee;
}
</style>
