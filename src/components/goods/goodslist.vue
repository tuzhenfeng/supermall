<template>
    <div class="goods">
        <goodslistitem v-for="item in goods" :key="item.id" :goodsitem="item" />
    </div>
</template>
<script>
import goodslistitem from './goodslistitem'
export default {
    components:{
        goodslistitem
    },
    data(){
        return {

        }
    },
    props:{
        goods:{
            type:Array,
            dafault(){
                return []
            }
        }
    }
}
</script>
<style>
.goods{
    padding-left: 8px;
    box-sizing: border-box;
}
</style>