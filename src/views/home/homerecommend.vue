<template>
    <div class="recommend">
        <div v-for="item in recommend" :key="item.id" class="recommend-item">
            <a :href="item.link"></a>
            <img :src="item.image" alt="">
            <div class="title">{{item.title}}</div>
        </div>
    </div>
</template>
<script>
export default {
    name:"recommends",
    props:{
        recommend:{
            type:Array,
            dafault(){
                return[]
            }
        }
    }
}
</script>
<style>
.recommend{
    display: flex;
    width: 100%;
    text-align: center;
    font-size: 12px;
    padding: 10px 0 ;
    border-bottom: 8px solid #eee;
}
.recommend-item{
    flex: 1;
}
.recommend-item img{
    width: 70px;
    height: 70px;
}
.recommend-item .title{
    margin-top: 10px;
}
</style>