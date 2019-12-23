<template>
  <div id="home">
    <navbar class="home-nav">
      <div slot="center">购物街</div>
    </navbar>
    <scroll class="content" ref="scroll" :probe-type="3" @scroll="contentscroll" @pullingUp="lodemore" :pull-up-load="true">
      <homeswiper :banners="banners"></homeswiper>
      <homerecommend :recommend="recommends"></homerecommend>
      <div class="recommend_bg">
        <img src="~assets/img/home/recommend_bg.jpg" alt />
      </div>
      <tabcontrol @tabclick="tabclick" class="tabcontrol" :title="['流行','新款','精选']"></tabcontrol>
      <goodslist :goods="goods[currentType].list"></goodslist>
    </scroll>
    <backtop @click.native="backclick" v-if="show" />
  </div>
</template>

<script>
import homeswiper from "./childComponents/homeswiper";
import homerecommend from "./homerecommend";
import { getHomeMultidata, gethomegoods } from "../../network/home";
import goodslist from "../../components/goods/goodslist";
import navbar from "../../components/common/navbar/navbar";
import tabcontrol from "../../components/tabcontrol/tabcontrol";
import scroll from "../../components/common/scroll/Scroll";
import backtop from "../../components/backtop/backtop";
export default {
  components: {
    navbar,
    tabcontrol,
    homeswiper,
    homerecommend,
    goodslist,
    scroll,
    backtop
  },
  data() {
    return {
      banners: [],
      recommends: [],
      goods: {
        pop: { page: 0, list: [] },
        new: { page: 0, list: [] },
        sell: { page: 0, list: [] }
      },
      currentType: "pop",
      show: false
    };
  },
  created() {
    this._getHomeMultidata();
    this._gethomegoods("pop");
    this._gethomegoods("new");
    this._gethomegoods("sell");
  },
  methods: {
    // ------------事件监听--------------
    tabclick(index) {
      switch (index) {
        case 0:
          this.currentType = "pop";
          break;
        case 1:
          this.currentType = "new";
          break;
        case 2:
          this.currentType = "sell";
          break;
      }
    },
    backclick() {
      // 组件内不能直接监听点击   如果想要监听需要使用native属性来监听原生组件点击事件
      this.$refs.scroll.scrollTo(0, 0, 500);
    },
    contentscroll(position) {
      this.show = -(position.y) > 1000
    },
    lodemore(){
      this._gethomegoods(this.currentType)
    },
    // -------网络请求------------------
    _getHomeMultidata() {
      getHomeMultidata().then(res => {
        this.banners = res.data.banner.list;
        this.recommends = res.data.recommend.list;
      });
    },
    _gethomegoods(type) {
      const page = this.goods[type].page + 1;
      gethomegoods(type, page).then(res => {
        this.goods[type].list.push(...res.data.list);
        this.goods[type].page += 1;
        this.$refs.scroll.finishPullUp()
      });
    }
  }
};
</script>
<style scoped>
#home {
  padding-top: 44px;
  padding-bottom: 60px;
  height: 100vh;
  position: relative;
}
.home-nav {
  background-color: var(--color-tint);
  color: #fff;
  position: fixed;
  top: 0;
  left: 0;
  z-index: 1;
  width: 100%;
}
.recommend_bg {
  width: 100%;
}
.recommend_bg img {
  width: 100%;
}
.tabcontrol {
  position: sticky;
  top: 44px;
  background-color: #fff;
  z-index: 1;
}
.content {
  overflow: hidden;
  position: absolute;
  top: 44px;
  bottom: 49px;
  left: 0;
  right: 0;
}
</style>

