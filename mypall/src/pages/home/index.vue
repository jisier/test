<template>
    <div>
      <my-scroll class="wrapper" 
      :data="productData" 
      :listenScroll="isScroll"
      @scroll="_scroll"
      :pullup="pullup" 
      @pullup="_pullup" 
      ref="scroll">
         <div class="content">
            <!-- nav-bar 内容 -->
            <nav-bar>
                <img src="./images/fenlei.png" alt="" slot="left">
                <img src="./images/logo.png" slot="center" style="margin-top:10px">
                <a href="" slot="right">登录</a>
            </nav-bar>
            <div class="title-sousuo">
                    <div class="input">
                        <input type="text">
                        <i class="iconfont icon-sousuo1"></i>
                        <span>搜索商品、品牌</span>
                    </div>
                </div>
            <nav class="nav">
                <ul class="nav-list">
                    <li class="nav-item" v-for="(val,key) in navs" :key="key">
                        <a href="#" class="nav-link">
                            <img :src="val.navurl" class="nav-pic">
                            <span>{{val.title}}</span>
                        </a>
                    </li>
                </ul>
            </nav>
            <swiper :options="swiperOption">
                <swiper-slide v-for="(val,key) in sliders" :key="key">
                    <a :href="val.imgurl">
                        <img :src="val.imgName" alt>
                    </a>
                </swiper-slide>
                <div class="swiper-pagination" slot="pagination"></div>
            </swiper>
            <div class="datu">
                <a href="">
                    <img src="./images/datu.png">    
                </a>    
            </div>
            <product-list @loaded="getProductData" ref="productList"></product-list>
         </div>
      </my-scroll> 
      <div class="g-backtop-container">
         <me-backtop :visible="isBacktopVisible" @backtop="backToTop"/>
      </div>
    </div>
</template>

<script>
    import NavBar from "@/components/navbar";
    import MyScroll from "@/components/scroll";
    import MeBacktop from "@/components/backtop";
    import {swiper,swiperSlide} from "vue-awesome-swiper";
    import ProductList from "./productList.vue";
    export default {
        name: "home",
        components:{ 
            NavBar,
            MyScroll,
            swiper,
            swiperSlide,
            ProductList,
            MeBacktop
        },
        data(){
            return{
                isScroll:true,
                isBacktopVisible:false,
                productData:[],
                page:1,
                totalPage:0,
                pulldown:true,
                pullup:true,
                
                sliders:[
                    {
                        imgurl:"http://www.sohu.com",
                        imgName: require("./images/01.png")
                    },
                    {
                        imgurl:"http://www.baidu.com",
                        imgName: require("./images/02.png")
                    },
                    {
                        imgurl:"http://www.jd.com",
                        imgName: require("./images/03.png")
                    },
                    {
                        imgurl:"http://www.sohu.com",
                        imgName: require("./images/04.png")
                    },
                    {
                        imgurl:"http://www.baidu.com",
                        imgName: require("./images/05.png")
                    },
                    {
                        imgurl:"http://www.jd.com",
                        imgName: require("./images/06.png")
                    },
                    {
                        imgurl:"http://www.tmall.com",
                        imgName: require("./images/07.png")
                    }
                ],
                swiperOption:{
                    direction:"horizontal",
                    loop:true,
                    pagination:{
                        el:".swiper-pagination"
                    },
                    autoplay:{
                        delay:2500,
                        disableOnInteraction:false
                    }
                },
                navs:[
                    {
                        navurl:require("./images/title1.png"),
                        title:"苏宁易购"
                    },
                    {
                        navurl:require("./images/title2.png"),
                        title:"天猫超市"
                    },
                    {
                        navurl: require("./images/title3.png"),
                        title: "天猫国际"
                    },
                    {
                        navurl: require("./images/title4.png"),
                        title: "聚划算"
                    },
                    {
                        navurl: require("./images/title5.png"),
                        title: "分类"
                    }
                ]
                
            };
        },
        methods:{
            getProductData(obj) {
                this.productData = obj.productList;
                this.page = obj.page;
                this.totalPage = obj.totalPage;
            },
            _scroll(pos){
                console.log(pos);
                console.log(pos.y);
                this.isBacktopVisible = pos.y < 0 && -pos.y >200;
            },
            _pulldown(){
                console.log("正在下拉");
            },
            _pullup(){
                console.log("正在上拉");
                if(this.page > this.totalPage){
                    console.log("没有更多了");
                    this.pullup = false;
                    return false;
                }
                this.$refs.productList.update();
            },
            backToTop(){
                this.$refs.scroll && this.$refs.scroll.scrollTo(0,0);
            }
        }
    };
</script>

<style scoped>
.navbar {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: row;
  height: 82px;
  background-color: #f60;
}
/* .search-box-wrapper {
  display: flex;
  align-items: center;
  padding: 7px;
  background-color: #fff;
} */
.g-container .iconfont {
  color: #fff;
  font-size: 30px;
}
.search-box-wrapper .iconfont {
  color: #ccc;
  font-size: 20px;
  font-weight: bold;
}
.search-box {
  flex: 1;
  background: none;
  border: none;
  margin: 0 9px;
  color: #666;
  line-height: 1.5;
}
/*轮播图*/
.swiper-container {
  width: 96%;
  height: 160px;
  padding-top: 0.3rem;

}
.swiper-container img {
  width: 100%;
  height: 100%;
}
/*nav 导航样式*/
.nav {
  width: 100%;
  padding-top: 0.3rem;
  background-color: #fff;
}

.nav-list {
  display: flex;
  flex-wrap: wrap;
}

.nav-item {
  width: 20%;
  margin-bottom: 0.15rem;
}

.nav-link {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
.nav-pic {
  width: 60%;
  margin-bottom: 0.3rem;
}
.datu{
        display: flex;
        width:96%;
        min-height:175px;
        align-items: center;
        justify-content: center;
        margin:0 auto;
    }
.datu img{
        width:100%;
        height:100%;
    }
.title-sousuo{
    text-decoration: none;
    box-sizing: border-box;
    align-self: center;
    padding: 0px 10.6667px 10.6667px;
    display: flex;
     background-color: rgb(255, 0, 54);
    flex-direction: row;
    width: 100%;
    margin:0 auto;
    position: relative;
    min-height: 49.0667px;
  }
  .title-sousuo>.input{
    position: relative;
    box-sizing: border-box;
    display: flex;
    flex-direction: row;
    align-content: flex-start;
    flex: 1 1 0%;
  border-radius: 5px;

    background-color: rgb(255, 255, 255);
    -webkit-box-flex: 1;
    position: relative;
  }
  .title-sousuo>.input>input{
      height:100%;
      position: absolute;
      top:0;
      left:30px;
  }
  .title-sousuo>.input>span{
    white-space: pre-wrap;
    position: relative;
    box-sizing: border-box;
    display: flex;
    -webkit-box-orient: vertical;
    flex-direction: column;
    align-content: flex-start;
    flex-shrink: 0;
    font-size: 12px;
    background-color: transparent;
    align-self: center;
    line-height: 40.5333px;
    color: rgba(0, 0, 0, 0.3);
  }
  .icon-sousuo1{
    width:16px;
    color:#ccc;
    height:17px;
    display: flex;
    position: relative;
    margin: 4.6667px 17px 0 6px;
    font-size: 28px;
  }
  .wrapper {
  width: 100%;
  height: 1000px;
  overflow: hidden;
}
.content {
  height: auto;
}
</style>