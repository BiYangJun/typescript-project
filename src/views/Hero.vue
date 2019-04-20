<template>
  <div>
    <p>欢迎来到{{wordname}}</p>
    <div v-if="step==1">
      <p>选择身份</p>
      <div>
        <input type="radio" value="hero" id="hero" v-model="role.type" >
        <label for="hero">英雄</label>

        <input type="radio" value="slime" id="slime" v-model="role.type">
        <label for="slime">史莱姆</label>
      </div>
      <div>{{computedname}}</div>
      <div>
        <label for="name">名字:</label>
        <input type="text" id="name" v-model="role.name" ref='nameinput'>
        <br>
        <label for="hp">血量:</label>
        <input type="text" id="hp" v-model="role.hp">
        <br>
        <label for="age">年龄:</label>
        <input type="text" id="age" v-model="role.age">
        <br>
        <button @click="submitRoleInfo">确定</button>
      </div>
    </div>
    <div v-if="step>=2">
        <p>角色信息</p>
        <p>name:{{hero.name}},hp:{{hero.hp}},age:{{hero.age}}</p>
    </div>
    <div v-if="step==2">
      <button @click="gopersoncity(hero)">前往人类城镇</button>
      <button @click="gomonstercity(hero)">前往怪物城镇</button>
    </div>

    <test ref="testcomponent"></test>
  </div>
</template>
<script lang="ts">
import { Component, Vue, Prop ,Watch} from "vue-property-decorator";
import test from '@/components/test.vue'
interface HeroConfig {
  type: string;
  name: any;
  hp: any;
  age?: any;
  [propName: string]: any;
}

class Hero {
  name: string;
  private hp: number; //当成员被标记成 private时，它就不能在声明它的类的外部访问。表示私有属性
  age?: number;
  constructor(name: string, hp: number, age?: number) {
    this.name = name;
    this.hp = hp;
    this.age = age;
  }
}
class Slime {
  name: string;
  private hp: number; //当成员被标记成 private时，它就不能在声明它的类的外部访问。表示私有属性
  age?: number;
  constructor(name: string, hp: number, age?: number) {
    this.name = name;
    this.hp = hp;
    this.age = age;
  }
}

class Warrior extends Hero {
  weapon: string;
  constructor(name: string, hp: number, weapon: string) {
    super(name, hp);
    this.weapon = weapon;
  }
  swing() {
    console.log("swing");
  }
}

@Component({
  name: "HeroGame",
  components:{
      test
  }
})
export default class HeroGame extends Vue {
    $refs!:{
        nameinput:HTMLInputElement,
        testcomponent:test
    }
  // props
  @Prop({
    type: String,
    default: "中土世界"
  })
  wordname!: string;
  // watch
  @Watch('role.type')
  watchRoleType(newVal:string,oldVal:string):void{
      console.log('watchRoleType'+newVal)
  }   
  @Watch('role',{deep:true})
  watchRole(newVal:HeroConfig,oldVal:HeroConfig):void{
      console.log(newVal)
  }
  // computed
  get computedname():string{
      return 'type:'+this.role.type
  }
  set computedname(val:string){ //注意，这里不能标返回值类型，就算写void也不行
    console.log(val)
  }
  // data
  role: HeroConfig = { type: "", name: "", hp: "", age: "" };
  hero: object = {};
  step: number = 1;
  mounted() {}
  submitRoleInfo(): void {
    if (this.role.type == "hero") {
      this.hero = this.createHero(this.role);
    } else if (this.role.type == "slime") {
      this.hero = this.createSlime(this.role);
    }
    this.step = 2;
    this.test();
  }
  createHero(hero: HeroConfig): object {
    return new Hero(hero.name, hero.hp, hero.age);
  }
  createSlime(hero: HeroConfig): object {
    return new Slime(hero.name, hero.hp, hero.age);
  }
  gopersoncity(role: Hero) {
    
  }
  gomonstercity(role: Slime) {
      
  }
    test():void{
        this.$refs.nameinput.blur() 
        this.$refs.testcomponent.handle()
    }
  forest(hero: Hero) {}
  throwError(message:string):never{
      throw new Error(message)
  }
}
</script>