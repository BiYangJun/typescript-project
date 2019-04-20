<template>
  <div class="home">
    <input type="text" v-model="msg">
    <p>props:{{propMessage}}</p>
    <p>data:{{msg}}</p>
    <p>computed:{{computedMsg}}</p>
    <p @click="handlegreet">methods</p>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import HelloWorld from '@/components/HelloWorld.vue'; // @ is an alias to /src
@Component({
  components: {
    HelloWorld
  },
  props:{
    propMessage:String
  }
})
export default class Home extends Vue {
  msg = 123
  message:string = 'hello'
 
  mounted(){
    this.fooFn(1)
    this.throwError('这是一个error')
    let isBol:boolean = false;
    let isStr:string = '1';
    let isNum:number = 1;
    let isList1:string[] = ['1','2','3'];
    let isList2:Array<string> = ['1','3','2'];
    let isList3:any[] = [1,'2',false];
    let isList4:ReadonlyArray<any> = isList3 //只读数组
    let tuple:[string,number] //元组 tuple['1',1] true
    enum Color {Red,Green,Blue}
    let notSure:any = 4;
    let unusable:void = undefined;

    interface SquareConfig{
      color:string; //必选属性
      width?:number; //可选属性
      readonly x:number; //只读属性
      [propName:string]:any; //任意数量的其他属性
    }
    function createSquare(config:SquareConfig):{color:string;area:number}{
      let newSquare = {color:'green',area:100}
      return newSquare
    }
  }
  // computed
  get computedMsg(){
    return 'computed'+this.msg
  }
  //method
  handlegreet(){
    alert(this.msg)
  }
  fooFn(str:number){
    console.log(str)
  }
  f([a,b]:[string,number]):string{
    return ''
  }
  warnUser():void{
    //void类型像是与any类型相反，它表示没有任何类型。 当一个函数没有返回值时，你通常会见到其返回值类型是 void
    console.log('this')
  }
  throwError(message:string):never{
    throw new Error(message)
  }
  
}
</script>
