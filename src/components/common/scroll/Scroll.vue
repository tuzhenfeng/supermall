<template>
<!-- ref/dhildren 一般绑定在组件上 -->
  <div class="wrapper" ref="wrapper">
    <div class="content">
      <slot></slot>
    </div>
  </div>
</template>
<script>
import BScroll from 'better-scroll'
export default {
  name: "scroll",
  props:{
      probeType:{
          type:Number,
          dafault:0
      },
      pullUpLoad:{
          dafault:false
      }
  },
  data(){
      return {
          scroll:null
      }
  },
  mounted(){
    //   创建bscroll
      this.scroll = new BScroll(this.$refs.wrapper,{
          click:true,
          probeType:this.probeType,
          pullUpLoad:this.pullUpLoad
      })

    //  监听滚动的位置
    this.scroll.on('scroll',(position)=>{
        this.$emit('scroll',position)
    }) 
    // 监听上拉事件
    this.scroll.on('pullingUp',()=>{
        console.log('上拉加载更多')
        this.$emit('pullingUp')
    })
  },
  methods:{
      scrollTo(x,y,time){
          this.scroll.scrollTo(x,y,time)
      },
      finishPullUp(){
          this.scroll.finishPullUp()
      }
  }
};
</script>
<style scoped>
</style>