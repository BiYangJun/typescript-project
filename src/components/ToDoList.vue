<template>
    <div>
        <button @click="createword" v-if="!createstatus">创建一个魔幻世界</button>
        <template v-if="createstatus">
            <div >创建成功！</div>
            <Hero :wordname='createname' ></Hero>
        </template>
    </div>
</template>
<script lang='ts'>
import { Component, Vue } from 'vue-property-decorator';
import Hero from '@/views/Hero.vue';
@Component({
    name:'todolist',
    components:{
        Hero
    }
})
export default class ToDoList extends Vue{
    createname:any = ''
    createstatus:boolean = false
    createword():void{
        let name = prompt('请输入世界名称');
        console.log(name)
        this.createname = name;
        this.createstatus = typeof name=='string' ? true : false;
    }
}
</script>