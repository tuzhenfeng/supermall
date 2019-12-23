<template>
    <div class="tabcontrol">
        <div @click="itemclick(index)" v-for="(item,index) in title" :key="index" class="tabitem" :class="{active:isactiveindex==index}">
            <span>{{item}}</span>
        </div>
    </div>
</template>
<script>
export default {
    name:'tabcontrol',
    props:{
        title:{
            type:Array,
            default:{
                return:[]
            }
        }
    },
    data(){
        return{
            isactiveindex:0
        }
    },
    methods:{
        itemclick(index){
            this.isactiveindex=index
            this.$emit('tabclick',index)
        }
    }
}
</script>
<style >
.tabcontrol{
    display: flex;
}
.tabitem{
    height: 44px;
    line-height: 44px;
    font-size: 15px;
    flex: 1;
    text-align: center;
}
.tabitem span{
    border-bottom: 1ps solid 
}
.active{
    color: var(--color-high-text)
}
.active span{
    padding: 5px;
    border-bottom:3px solid var(--color-high-text);
}
</style>