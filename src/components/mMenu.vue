<template>
  <div class="m-cont">
    <div class="m-wrap" v-for="(item,i) in menuList" :key="item.name">
      <p class="m-text">{{ item.name }}</p>
      <div class="m-tlist">
        <div v-for="(items,s) in item.list" :key="items.names" class="m-item">
          <div class="m-items">{{ items.names }}</div>
          <div class="m-items">{{ items.val }}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "mMenu",
  data() {
    return {
      menuList: [
        {
          name: '菜单',
          list: [{
            names: '数量加',
            val: '+'
          },
            {
              names: '数量减',
              val: '-'
            },
            {
              names: '数量',
              val: '+'
            },
            {
              names: '无码商品',
              val: 'W'
            },
            {
              names: '删除',
              val: 'I'
            },
            {
              names: '退货',
              val: 'A'
            },
            {
              names: '挂单',
              val: 'R'
            },
            {
              names: '回复挂单',
              val: 'O'
            },
            {
              names: '查询订单',
              val: 'R'
            },
            {
              names: '查询库存',
              val: 'N'
            },
          ]
        },
        {
          name: '优惠',
          list: [{
            names: '优惠',
            val: '/'
          },
            {
              names: '整单优惠',
              val: 'Z'
            },
            {
              names: '赠送',
              val: 'S'
            },
            {
              names: '积分兑换',
              val: 'D'
            },
          ]
        },
        {
          name: '会员',
          list: [{
            names: '会员交易',
            val: 'M'
          },
            {
              names: '添加会员',
              val: 'F8'
            },
            {
              names: '会员储值',
              val: 'K'
            },
            {
              names: '',
              val: ''
            },
          ]
        },
      ]
    }
  },
}
</script>

<style scoped>
.m-cont {
  padding-left: 23px;
  color: #333333;
  text-align: left;
}

.m-wrap {
  min-width: 380px;
  margin-top: 30px;
}

.m-tlist {
  display: flex;
  align-items: center;
  flex-wrap: wrap;
  border-left: 1px solid #d8d8d8;
}

.m-text {
  padding-left: 8px;
  font-size: 16px;
  font-weight: 700;
}

.m-item {
  display: flex;
  align-items: center;
}

.m-items {
  display: flex;
  width: 90px;
  height: 35px;
  font-size: 14px;
  justify-content: center;
  align-items: center;
  background: #e2e2e2;
  border-right: 1px solid #d8d8d8;
  border-bottom: 1px solid #d8d8d8;
}
.m-tlist .m-item:nth-child(-n+2) .m-items{
  border-top: 1px solid #d8d8d8;
}
.m-items:nth-child(2n) {
  background: #fff;
}
</style>
