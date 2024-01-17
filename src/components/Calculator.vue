<script>
import ButtoNum from "./ButtoNum.vue"
export default {
  name:"Calculator",
  components:{ButtoNum},
  data(){
    return {
      evaluation:"",
      result:"",
      buttons:['7','8','9','+','4','5','6','-','1','2','3','*','0','.','=','/']
    }
  },
  methods:{
    handleClick(symbol){
      console.log(this.evaluation);
      if(this.result){
        if(Number(symbol) === +symbol) this.evaluation = symbol
        else this.evaluation = ""
        this.result = ""
      }else{
        if(symbol == "="){
          if(this.evaluation)this.result = eval(this.evaluation)
          else this.result = ""
          this.evaluation = this.result
        }else{
          if(!this.evaluation){
            if(Number(symbol) === +symbol) this.evaluation += symbol
          }else{
            const operations = ['+','-','*','/']
            if(Number(this.evaluation[this.evaluation.length-1]) === +this.evaluation[this.evaluation.length-1]){
              this.evaluation += symbol
            }
            if(this.evaluation[this.evaluation.length-1] == "."){
              if(!operations.includes(symbol) && symbol != ".") this.evaluation += symbol
            }
            if(operations.includes(this.evaluation[this.evaluation.length-1])){
              if(!operations.includes(symbol) && symbol != ".") this.evaluation += symbol
            }
          }
        }
      }
    }
  }
}
</script>

<template>
<div id="calculator">
  <div id="operation">{{evaluation}}</div>
  <div id="buttons">
    <ButtoNum v-for="(button, index) in buttons" :text="button" @clickYay="handleClick"></ButtoNum>
  </div>
</div>
</template>

<style scoped>
#calculator{
  width: 215px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  border-radius: 10px;
  gap: 10px;
}
#operation{
  width: 100%;
  min-height: 50px;
  border: 0;
  box-shadow: 3px 3px 3px gray;
  background-color: white;
  border-radius: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  word-wrap: break-word;
  word-break: break-all;
  box-sizing: border-box;
  padding: 10px;
}
#buttons{
  width: 100%;
  display: grid;
  grid-template-columns: repeat(4, 50px);
  grid-template-rows: repeat(4, 50px);
  row-gap: 5px;
  column-gap: 5px;
}
</style>
