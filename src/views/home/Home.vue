<template>
  <div id="home" class="wrapper">
    <navbar class="home-nav">
      <div slot="center">购物街</div>
    </navbar>
    <home-swiper :banners="bannerList"/>
    <recommend  :recommends="recommendList"/>
    <feature-view />
    <tab-control :titles="titleList"
                 class="tab-control"
                 @tabClick="tabClick" />
    <goods-list :goods="goods[currentType].list"></goods-list>
  </div>
</template>

<script>
  import navbar from '../../components/common/navBar/NavBar'
  import TabControl from '../../components/content/tabControl/TabControl'
  import GoodsList from '../../components/content/goods/GoodsList'
  import HomeSwiper from './childComps/HomeSwiper'
  import Recommend from './childComps/RecommendView'
  import FeatureView from './childComps/FeatureView'

  import {getHomeMultiData,getHomeGoods} from "../../network/home";
  export default {
    name:"Home",
    components:{
      navbar,
      HomeSwiper,
      Recommend,
      FeatureView,
      TabControl,
      GoodsList
    },
    data() {
      return {
        bannerList:[],
        recommendList:[],
        titleList:["流行","新款","精选"],
        goods:{
          'pop':{page:0,list:[]},
          'new':{page:0,list:[]},
          'sell':{page:0,list:[]},
        },
        currentType:"pop"
      }
    },
    created() {
     this.getMulitiData();
     this.getHomeGoods('pop');
     this.getHomeGoods('new');
     this.getHomeGoods('sell');
    },
    methods:{
      tabClick(index) {
        switch (index) {
          case 0:
            this.currentType = 'pop';
            break
          case 1:
            this.currentType = 'new';
            break
          case 2:
            this.currentType = 'sell';
            break
        }
      },
      getMulitiData() {
        getHomeMultiData().then(resp => {
          if(resp.data) {
            //获取轮播图数据
            this.bannerList = resp.data.banner.list;
            this.recommendList = resp.data.recommend.list;
          }
        })
      },
      getHomeGoods(type) {
        const page = this.goods[type].page+1;
        getHomeGoods(type,page).then(resp => {
          this.goods[type].list .push(...resp.data.list);
          this.goods[type].list .page+=1;
        })
      }
    }
  }
</script>

<style scoped>
  #home {
    padding-top: 44px;
  }
  .home-nav {
    background-color:var(--color-tint);
    color:#fff;
    position: fixed;
    left: 0;
    right: 0;
    top: 0;
    z-index: 9999;
  }
  .tab-control {
    position: sticky;
    top: 44px;
    z-index: 9;
  }
</style>
