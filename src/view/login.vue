<template>
  <div class="cont">
    <div class="cont-wrap">
      <div class="cont-w-l"></div>
      <div class="cont-w-r">
        <p class="contname">XXX智慧收银系统</p>
        <m-input class="cont-w-i" mValue='admin' :pMsg="pMsg"></m-input>
        <m-input class="cont-w-i" mValue="123456" :pMsg="pMsgp"></m-input>
        <m-btn @mClick="toPage" :tMsg=tMsg></m-btn>
      </div>
    </div>
  </div>
</template>

<script>
import mInput from '@/components/mInput';
import mBtn from '@/components/mBtn';
export default {
  name: "login",
  components: {
    mInput,
    mBtn
  },
  data () {
    return {
      tMsg:'登录',
      pMsg:'账号',
      pMsgp:'密码'
    }
  },
  methods:{
    toPage(){
      this.$router.push('/home')
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.cont{
  display: flex;
  width: 100vw;
  height: 100vh;
  font-family: 'siyuan';
  align-items: center;
  justify-content: center;
  background: url("../assets/login_bg.png") no-repeat;
  background-size: 100% 100%;
}
.cont-wrap{
  display: flex;
  width: 980px;
  height: 478px;
  background: #ffffff;
  border-radius: 16px;
}
.cont-w-l{
  width: 623px;
  height: 474px;
  background: url("../assets/login_box.png") no-repeat;
  background-size: 100% 100%;
}
.cont-w-r{
}
.cont-w-r .contname{
  width: 288px;
  height: 50px;
  margin: 68px 0 50px 7px;
  font-size: 36px;
  font-weight: 400;
  text-align: left;
  color: #333333;
}
.cont-w-i{
  margin-bottom: 24px;
}
</style>

