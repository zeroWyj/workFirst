<template>
  <div>
    <button  @click="mClick" class="t">{{tMsg}}</button>
  </div>
</template>

<script>
export default {
  name: "mBtn",
  props: {
    tMsg: {
      type: String,
      default: ''
    },
  },
  methods:{
    mClick(data){
      this.$emit('mClick', data)
    },
  }
}
</script>

<style scoped>
button{
  border: none;
  padding: 0;
}
.t{
  display: block;
  width: 300px;
  height: 45px;
  font-size: 18px;
  font-weight: 500;
  color: #ffffff;
  background: #1ed5b3;
  border-radius: 6px;
  box-shadow: 0 6px 10px 0 rgba(30,213,179,0.20);
  cursor: pointer;
}
.t:hover{
  background-color: #51E5C9;
}
</style>

