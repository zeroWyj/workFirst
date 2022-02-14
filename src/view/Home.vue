<template>
  <div class="cont">
    <div class="top">
      <div class="top-l">
        <div class="top-l-wrap">
          <div class="top-name">【万顺连锁超市-成都西站店】</div>
          <div class="top-text">订单号：20201221143123001</div>
          <div class="top-text"><i class="top-i"></i>{{ nowTime }}</div>
        </div>
        <div>
          <m-btn class="t-btn" tMsg='挂单(0)'></m-btn>
        </div>
      </div>
      <div class="top-r">
        <div class="flex">
          <i class="top-i top-iuser"></i>
          <p>收银员：刘备</p>
        </div>
        <div class="flex">
          <i class="top-i top-imsg"></i>
          <i class="top-i top-ipath"></i>
          <i class="top-i top-iinter"></i>
          <i class="top-i top-iinter_forbidden"></i>
        </div>
      </div>
    </div>
    <div class="wrap">
      <div class="w-l">
        <div class="w-tab">
          <table>
            <thead>
            <tr>
              <td>序号</td>
              <td>条形码</td>
              <td>商品名称</td>
              <td>数量</td>
              <td>单价</td>
              <td>现价</td>
              <td>小计</td>
            </tr>
            </thead>
            <tbody>
            <tr v-for="(item,i) in tabList" :key="i" :class="nowIndex === i?'w-tab-active':''">
              <td>{{ i + 1 }}</td>
              <td>{{ item.code }}</td>
              <td>{{ item.name }}</td>
              <td>{{ item.quantity }}</td>
              <td>{{ item.price }}</td>
              <td>{{ item.priceNow }}</td>
              <td>{{ (item.priceNow * item.quantity).toFixed(2) }}</td>
            </tr>
            </tbody>
          </table>
        </div>
        <div class="foot">
          <div class="f-top">
            <div class="flex">
              <span>商品条形码：</span>
              <m-input ref="mInput" @keyDowns="keyDowns" pMsg="请扫描或输入商品条形码，输入后按Enter键。" :mValue.sync="mValue"
                       class="f-inp"></m-input>
            </div>
            <m-btn class="f-btn" tMsg='结算模式'></m-btn>
          </div>
          <div class="flex f-bwrap">
            <div class="f-btns"><span>找零：</span><span class="f16">￥</span>00.00</div>
            <div class="f-btns"><span>应收：</span><span class="f16">￥</span>{{ totalPrice || '00.00' }}</div>
          </div>
        </div>
      </div>
      <div :class="['w-r',isShow?'':'w-ractive']">
        <div class="flex w-rtop" v-if="isShow">
          <m-btn @mClick="showMore()" class="f-rtbtn" tMsg='收起(F1)'></m-btn>
          <div class="f-rtoptext">常用快捷键(F1)</div>
        </div>
        <mMenu v-if="isShow"></mMenu>
      </div>
    </div>
    <m-popup :isShowPo="isShowPo" @closePo="closePo"></m-popup>
  </div>
</template>

<script>
import mInput from '@/components/mInput';
import mBtn from '@/components/mBtn';
import mMenu from '@/components/mMenu';
import mPopup from '@/components/mPopup';

export default {
  name: "Home",
  components: {
    mInput,
    mBtn,
    mMenu,
    mPopup
  },
  data() {
    return {
      mValue: '',//输入框
      tabList: [],//列表数据
      allList: [{
        code: 123,
        name: '鸡蛋',
        quantity: 1,
        price: '100',
        priceNow: '55.55',
        total: ''
      },
        {
          code: 456,
          name: '白菜',
          quantity: 1,
          price: '100',
          priceNow: '66.66',
          total: ''
        }],
      nowIndex: 0,//当前选中
      totalPrice: 0,
      nowTime: '',
      isShow: true, //菜单栏状态
      isShowPo: false,
    }
  },
  created() {
    this.getTime()
  },
  mounted() {
    let _this = this
    document.onkeydown = function (event) {
      let key = event.keyCode;
      if (key === 27) {
        event.preventDefault();
        //esc退出
        console.log('退出')
        if (_this.tabList && _this.tabList.length) {
          _this.isShowPo = true
          return
        }
        _this.$router.push('/')
      } else if (key === 73) {
        event.preventDefault();
        //i 删除
        if (_this.tabList && _this.tabList.length) {
          _this.delList()
        }
        console.log('删除')
      } else if (key === 112 || key === 91) {
        event.preventDefault();
        //F1 显示隐藏
        _this.isShow = !_this.isShow
        console.log('显示隐藏')
      } else if (key === 38 && _this.tabList.length) {
        event.preventDefault();
        //上
        if (_this.nowIndex > 0) {
          _this.nowIndex--
        }
        console.log('上')
      } else if (key === 40 && _this.tabList.length) {
        event.preventDefault();
        //下
        if (_this.nowIndex < _this.tabList.length - 1) {
          _this.nowIndex++
        }
        console.log('下')
      }
    }
  },
  watch: {
    tabList: {
      handler(val) {
        if (val && val.length) {
          this.totalPrice = 0
          val.forEach(item => {
            this.totalPrice = (item.quantity * item.priceNow + Number(this.totalPrice)).toFixed(2)
          })
        } else {
          this.totalPrice = null
        }
        console.log(val)
      },
      deep: true
    }
  },
  methods: {
    closePo() {
      this.isShowPo = !this.isShowPo
    },
    showMore() {
      this.isShow = !this.isShow
    },
    //删除
    delList() {
      this.tabList.splice(this.nowIndex, 1)
      if (!this.nowIndex) {
        return
      }
      this.nowIndex--
    },
    //编码框事件
    keyDowns(data) {
      let newArr = this.allList.filter(item => item.code == data)
      if (newArr && newArr.length) {
        if (this.tabList && this.tabList.length) {
          let newArrs = this.tabList.filter(item => item.code == newArr[0].code)
          if (newArrs && newArrs.length) {
            this.tabList.forEach(item => {
              if (item.code == newArrs[0].code) {
                item.quantity++
              }
            })
          } else {
            this.tabList.push(...newArr)
          }
        } else {
          this.tabList.push(...newArr)
        }
        this.mValue = null;
        this.$refs.mInput.KeyClear();
      }
    },
    //时间
    getTime() {
      let year = new Date().getFullYear();
      let month = new Date().getMonth() + 1 < 10 ? "0" + (new Date().getMonth() + 1) : new Date().getMonth() + 1;
      let date = new Date().getDate() < 10 ? "0" + new Date().getDate() : new Date().getDate();
      let hh = new Date().getHours() < 10 ? "0" + new Date().getHours() : new Date().getHours();
      let mm = new Date().getMinutes() < 10 ? "0" + new Date().getMinutes() : new Date().getMinutes();
      let ss = new Date().getSeconds() < 10 ? "0" + new Date().getSeconds() : new Date().getSeconds();
      this.nowTime = year + "-" + month + "-" + date + "   " + hh + ":" + mm + ':' + ss;
    },
  },
}
</script>

<style scoped>
table {
  width: 100%;
  border-collapse: collapse
}

table thead {
  height: 34px;
  background: #c8c8c8;
}

table tbody tr td {
  padding: 8px;
  word-break: break-all;
}

.cont {
  /*display: flex;*/
  position: relative;
  width: 100%;
  max-height: 100vh;
  font-family: 'siyuan', 'Avenir', Helvetica, Arial, sans-serif;
}

.top {
  display: flex;
  align-items: center;
  text-align: left;
  width: 100%;
  height: 60px;
  color: #fff;
  background: #323232;
}

.top-l {
  display: flex;
  justify-content: space-between;
  width: 100%;
}

.top-i {
  display: inline-block;
  width: 20px;
  height: 20px;
  margin-right: 8px;
  background: url("../assets/clock.png") no-repeat center center;
  background-size: 14px 14px;
}

.top-iuser {
  background: url("../assets/personal.png") no-repeat center center;
  background-size: 20px 20px;
}

.top-imsg {
  margin-right: 30px;
  background: url("../assets/msg.png") no-repeat center center;
  background-size: 18px 20px;
}

.top-ipath {
  margin-right: 30px;
  background: url("../assets/path.png") no-repeat center center;
  background-size: 20px 20px;
}

.top-iinter {
  background: url("../assets/inter.png") no-repeat center center;
  background-size: 18px 20px;
}

.top-iinter_forbidden {
  background: url("../assets/inter_forbidden.png") no-repeat center center;
  background-size: 18px 20px;
}

.top-l-wrap {
  display: flex;
  align-items: center;
}

.top-r {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 410px;
  padding: 0 25px 0 40px;
  flex-shrink: 0;
}

.t-btn >>> .t {
  width: 88px;
  height: 31px;
  font-size: 14px;
  border-radius: 16px;
}

.f-btn >>> .t {
  width: 101px;
  height: 34px;
  font-size: 16px;
  background: #1ed5b3;
  border-radius: 17px;
}

.f-inp >>> .t {
  width: 622px;
  height: 36px;
  background: #ffffff;
  border: 1px solid #ebebeb;
  border-radius: 4px;
}

.f-rtbtn >>> .t {
  width: 116px;
  height: 33px;
  font-size: 14px;
  background: #1ed5b3;
  border-radius: 0;
}

.top-text {
  display: flex;
  align-items: center;
  font-size: 14px;
  font-weight: Normal;
  margin-left: 80px;
}

.top-name {
  font-size: 18px;
  font-weight: 700;
  color: #1ed5b3;
}

.wrap {
  display: flex;
  height: calc(100vh - 60px);
}

.w-tab {
  height: calc(100vh - 200px);
  overflow-y: auto;
}

.w-tab-active {
  background: #c5eee6;
}

.w-l {
  width: 100%;
  background: #f2f2f2;
}

.w-r {
  position: relative;
  width: 410px;
  height: calc(100vh - 60px);
  overflow-y: auto;
  overflow-x: hidden;
  background: #ffffff;
  border: 1px solid #ebebeb;
  box-shadow: -10px 0 6px 0 rgba(0, 0, 0, .04);
  flex-shrink: 0;
  transition: width 2s;
  -webkit-transition: width .3s;
}

.w-ractive {
  width: 0;
}

.w-ranim {
  transition: width 2s;
  -webkit-transition: width 2s;
}

.w-rtop {
  border-bottom: 1px solid #ebebeb;
}

.f-rtoptext {
  padding-left: 35px;
  font-size: 16px;
}

.foot {
  width: 100%;
  height: 140px;
  align-items: flex-end;
  background: #f2f2f2;
}

.f-top {
  display: flex;
  height: 40px;
  padding: 0 16px;
  align-items: center;
  justify-content: space-between;
  background: #e2e2e2;
}

.flex {
  display: flex;
  align-items: center;
}

.f-bwrap {
  margin-left: 10px;
}

.f-btns {
  display: flex;
  width: 50%;
  height: 95px;
  align-items: center;
  justify-content: center;
  font-size: 46px;
  margin: 5px 10px 0 0;
  color: #333333;
  background: #e2f3f0;
  border-radius: 10px;
}

.f-btns span {
  font-size: 20px;
  margin-right: 80px;
}

.f-btns:nth-child(2) {
  background: #1ed5b3;
  color: #fff;
}

.f-btns .f16 {
  font-size: 16px;
  margin: 0;
}
</style>
