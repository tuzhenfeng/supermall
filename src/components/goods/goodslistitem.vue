<template>
    <div class="goodsitem">
        <img :src="goodsitem.show.img" alt="">
        <div class="bot">
            <p>{{goodsitem.title}}</p>
            <span class="price">￥{{goodsitem.price}}</span>
            <span class="cfav">
                <img src="~assets/img/common/collect.svg" alt="">
                {{goodsitem.cfav}}
            </span>
        </div>
    </div>
</template>
<script>
export default {
    data(){
        return {
            
        }
    },
    props:{
        goodsitem:{
            type:Object,
            default(){
                return []
            }
        }
    },
    created(){
    }
}
</script>
<style>
.goodsitem{
    width: 50%;
    display: inline-block;
    padding-right: 8px;
    font-size: 14px;
    padding-bottom: 10px;
    position: relative;
}
.goodsitem img{
    width: 100%;
}
.goodsitem P{
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
    margin-bottom: 5px;
}
.goodsitem .bot{
    display: absolute;
    bottom: 0;
    left: 0;
}
.bot .price{
    color: var(--color-tint)
}
.cfav {
    margin-right: 20px;
    float: right;
}
.cfav img{
    width: 14px;
    height: 14px;
}
</style>