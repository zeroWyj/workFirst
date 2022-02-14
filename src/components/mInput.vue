<template>
  <div>
    <input class="t" @keyup.enter="keyDowns()" v-model.trim="mValues" :placeholder="pMsg"/>
  </div>
</template>

<script>
export default {
  name: "mInput",
  props: {
    pMsg: {
      type: String,
      default: ''
    },
    mValue: {
      type: String,
      default: ''
    },
  },
  data () {
    return {
      mValues:this.mValue
    }
  },
  methods:{
    keyDowns(data){
      this.$emit('keyDowns', this.mValues)
    },
    KeyClear(){
      this.mValues = '';
    }
  }
}
</script>

<style scoped>
input:focus-visible{
  outline:0;
}
.t{
  display: block;
  width: 300px;
  height: 45px;
  padding: 13px;
  font-size: 16px;
  background: #ffffff;
  border: 1px solid #707070;
  border-radius: 6px;
}
.t:hover,
.t:active{
  border-color: #1ED5B3;
}
</style>
