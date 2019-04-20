<template>
  <div class="about">
    <h1>This is an about page</h1>
  </div>
</template>
<script lang='ts'>

class Greeter {
  greeting:string;
  constructor(message:string){
    this.greeting = message
  }
  greet(){
    return 'hello,'+this.greeting
  }
}

class GreeterChild extends Greeter {
  constructor(name:string){
    super(name)
  }
  say(){
    return 'greeting' + this.greeting
  }
}
let greeter = new Greeter('hahaha')
let greetrchild = new GreeterChild('111')

console.log(greeter.greet())
console.log(greetrchild.say())
import { Component, Vue } from 'vue-property-decorator';
@Component({

})
export default class about extends Vue {
  mounted() {
    
  }
}

</script>