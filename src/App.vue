<template>
  <div class="wrapper">
    <!--第{{n}}手-->
    <div class="row">
      <Cell v-on:click="onClickCell(0,$event)" v-bind:n="n" v-bind:result="result"/>
      <Cell v-on:click="onClickCell(1,$event)" v-bind:n="n" v-bind:result="result"/>
      <Cell v-on:click="onClickCell(2,$event)" v-bind:n="n" v-bind:result="result"/>
    </div>
    <div class="row">
      <Cell v-on:click="onClickCell(3,$event)" v-bind:n="n" v-bind:result="result"/>
      <Cell v-on:click="onClickCell(4,$event)" v-bind:n="n" v-bind:result="result"/>
      <Cell v-on:click="onClickCell(5,$event)" v-bind:n="n" v-bind:result="result"/>
    </div>
    <div class="row">
      <Cell v-on:click="onClickCell(6,$event)" v-bind:n="n" v-bind:result="result"/>
      <Cell v-on:click="onClickCell(7,$event)" v-bind:n="n" v-bind:result="result"/>
      <Cell v-on:click="onClickCell(8,$event)" v-bind:n="n" v-bind:result="result"/>
    </div>
    <div style="margin-top:10px;">获胜方：{{result==null?'胜负未分':result}}</div>
    <Confirm ref="myConfirm" @userBehavior="userBehaviorFun"></Confirm>
  </div>
</template>

<script>
  import Cell from './Cell';
  import Confirm from './VueConfirm';

  export default {
    components:{ Cell,Confirm },
    data(){
      return { n:0,
      map:[
        [null,null,null],
        [null,null,null],
        [null,null,null],
      ],
        result:null
      };
    },
    methods:{
      onClickCell(i,text){
        console.log(i+'号被点击：'+text);
        this.map[Math.floor(i/3)][i%3] = text;
        this.n = this.n+1;
        this.tell();
        this.success();
      },
      success(){
        if(this.result!=null){
          this.$refs.myConfirm.show('获胜方：'+this.result, {
            type: 'confirm',
            confirmText: '重来',
            cancelText: '退出', // 取消按钮的文字
            titleText: '恭喜！',
            data: '获胜方：'+this.result
          })
        }
      },
      tell(){
        const map = this.map;
        for(let i = 0;i<=2;i++){
          if(map[i][0]!=null && map[i][0] ===map[i][1]&&map[i][1]===map[i][2]){
            this.result = map[i][0];
          }
        }

        for(let j = 0;j<=2;j++){
          if(map[0][j]!=null && map[0][j] ===map[1][j]&&map[1][j]===map[2][j]){
            this.result = map[0][j]
          }
        }

        if(map[0][0]!=null&&map[0][0] === map[1][1]&& map[1][1]===map[2][2]){
          this.result = map[0][0]
        }

        if(map[0][2]!=null&&map[0][2] === map[1][1]&& map[1][1]===map[2][0]){
          this.result = map[0][2]
        }
      },
      userBehaviorFun(type,data){
        console.log(type);
        if(type=='clickConfirm'){
          console.log(111);
          location.reload();
        }
      }
    }
  }
</script>

<style>
  .wrapper{
    text-align: center;
    margin-top:50px;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
  }
.row{
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: row;
  width: 310px;
  border-left: solid 10px #6C3C29;
  border-right: solid 10px #6C3C29;
  background: #6C3C29;
}
.row:nth-child(1){
  border-top: solid 10px #6C3C29;
  padding-top:3px;
}
  .row:nth-child(3){
    border-bottom: solid 10px #6C3C29;
    padding-bottom: 3px;
  }
</style>
