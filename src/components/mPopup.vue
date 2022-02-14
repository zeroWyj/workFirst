<template>
<div class="mp-cont" v-if="isShowPo">
  <div class="con">
    <div class="mp-top">
      <div>提示</div>
      <div @click="closePo()">X</div>
    </div>
    <div class="mp-ccont">
      <div class="mp-text"><span class="mp-i">!</span>有订单尚未完成，不能退出 ！</div>
      <m-btn @mClick="closePo()" class="mp-btn" tMsg='Enter/确定'></m-btn>
    </div>
  </div>
</div>
</template>

<script>
import mBtn from '@/components/mBtn';
export default {
  name: "mPopup",
  components: {
    mBtn,
  },
  props:{
    isShowPo: {
      type: Boolean,
      default: false
    }
  },
  methods:{
    closePo(){
      this.$emit('closePo', this.show)
    },
  }
}
</script>

<style scoped>
.mp-cont{
  position: fixed;
  display: flex;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  align-items: center;
  justify-content: center;
  background: rgba(0,0,0,.3);
}
.con{
  width: 500px;
  min-height: 200px;
  background-color: #fff;
}
.mp-top{
  display: flex;
  height: 40px;
  padding: 0 20px;
  color: #ffffff;
  font-size: 18px;
  justify-content: space-between;
  align-items: center;
  background: #1ed5b3;

}
.mp-text{
  margin-top: 50px;
  text-align: center;
}
.mp-i{
  display: inline-block;
  width: 20px;
  height: 20px;
  margin-right: 8px;
  font-size: 14px;
  color: #fff;
  background: #ffa41c;
  border-radius: 10px;
}
.mp-btn >>> .t {
  width: 120px;
  height: 36px;
  font-size: 16px;
  margin: 30px auto 0 auto;
  background: #1ed5b3;
  border-radius: 4px;
}
</style>
