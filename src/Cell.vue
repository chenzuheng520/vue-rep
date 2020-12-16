<template>
  <div>
  <div class="cell" v-on:click="clickSelf">
    <template v-if="a">{{text}}</template>
    <template v-else ></template>
  </div>
  </div>
</template>

<script>
  console.log(111);
  export default {
    props:["n","result"],
    data(){
      return { a:false ,text:""}
    },
    methods:{
      clickSelf(){
        if(this.text!=""){
          return;
        }
        if(this.result!=null){
          console.log(this.result);
          return;
        }
        this.a = true;
        this.text = this.n%2 ===0 ?'x':'o';
        this.$emit('click',this.text);
      }
    }
  }
</script>

<style>
  .cell{
    width:100px;
    height: 100px;
    border: solid 0px #000;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 50px;
    background: #F4C79E;
    margin: 1px;
  }
</style>
