<template>
    <div>
        <!-- 我是产品页{{this.$route.params.id}}{{this.$route.params.imgurl}} -->
        <nav-bar>
            <i class="iconfont icon-back" slot="left" @click="goBack"></i>
            <div slot="center">
                商品详情
            </div>
            <i class="iconfont icon-msg" slot="right"></i>
        </nav-bar>
		<me-scroll class="wrapper" ref="scroll" :style="{'height':maxheight}">

		    <div class="content">
				<div class="swiper">
		    	<img :src="`http:${this.product.baseinfo.picUrl}`" alt>
				<div class="detail_decoration">
		    		<div class="price">¥<em>{{this.product.price.actPrice}}</em>.00</div>
		    		<div class="msg">
		    			<div class="text" id="ysPrice">
		    				<span id="ysTips"></span>
		    				<del class="old_price">{{this.product.price.origPrice}}</del>
		    			</div>
		    			<div class="text">
		    				<span class="logo type_seckill">京东秒杀</span>
		    			</div>
		    		</div>
		    		<div class="countdown" id="specTimer" style>
		    			<p class="countdown_text">距秒杀结束还剩</p>
		    			<p class="countdown_nums" id="timeLimit">
		    				<span class="box">07</span>:
							<span class="box">29</span>:
							<span class="box">40</span>
		    			</p>
		    		</div>
		    	</div>
		    </div>
		    <div class="area">
		    	<div class="fn_wrap">
		            <h1 class="fn fn_goods_name" id="favWrap">
		                <div class="fn_text_wrap">{{this.product.name.shortName}}</div>
		                <a class="favour" href="javascript:void(0)">关注</a>
		            </h1>

		            <div class="J_ping desc right_shorter">
						<a href="#">{{this.product.merit.desc}}</a></div>
               </div>
		    </div>
			<div>
				<div class="button-block">
        			<span class="add" @click="addToCart">加入到购物车</span>
					<span class="add" @click="addToCart">立即购买</span>
      			</div>
			</div>
		    </div>

		</me-scroll>
    </div>
</template>

<script>
import MeScroll from "@/components/scroll";
import NavBar from "@/components/navbar";
    export default {
	   name: "product",
	   data(){
		   return{
			   buyNum:1,
			   maxheight:document.documentElement.clientHeight - 100 + 'px'
		   };
	   },
       components: {
		   NavBar,
		   MeScroll
	   },
	   methods:{
		   goBack(){
			   this.$router.go(-1);
		   },
		   addToCart(){
			   let productInfo = {
				   id:this.$route.params.id,
				   img:this.product.baseinfo.picUrl,
				   title:this.product.name.shortName,
				   type:this.$route.params.id,
				   quantity:this.buyNum,
				   price:this.product.price.actPrice,
				   inventory:this.product.baseinfo.stock,
				   isCheck:false
			   };
			   this.$store.dispatch("addToCart",productInfo);
			   console.log("添加到购物车成功！");
		   }
	   },
	   computed:{
		   product(){
			   return this.$store.state.productInfo;
		   }
	   }
    };
</script>

<style scoped>
/* .all{
	height:100%;
} */
.content{
	height:auto;
}
.wrapper {
  width: 100%;
  /* height: 500px; */
  /* overflow: hidden; */
}
.button-block{
	display:fiex;
}
.add{
	display:inline-block;
	flex:1;
	text-align:center;
	font-size:20px;
	line-height: 1rem;
	padding:0px 20px;
	cursor:pointer;
	margin:0 10px;
}
.add:first-child{
	background:#fff1f5;
	color: #e93b3d;
}
.add:last-child{
	background:#e93b3d;
	color:#fff;
}
.navbar {
		    display: flex;
		    justify-content: center;
		    align-items: center;
		    flex-direction: row;
		    height: 50px;
		    background:linear-gradient(#eee,#ddd);
		    border-bottom:1px solid #ddd;
		    box-shadow: 0 2px 1px #ddd;
	   }
   	   .navbar-left {
	        margin-left: 0.1rem;
	        margin:0 0 0 10px;
		    width: 20px;
		    height: 20px;
		    font-size:24px;/*no*/
		    background-position: 0 0;
		    background-size: contain;
	   }
	.fenlei .iconfont,.login .iconfont,.logo div{
		font-size: 20px;/*no*/
	}
	   .navbar-center {
	      flex: 1;
	      margin: 0 0.1rem;
	      text-align: center;
	      font:18px 微软雅黑;
	   }
	    .navbar-right {
	      margin-right: 0.1rem;
	    }
	    .navbar .iconfont{
	    	font-size:20px;
	    }
	    .icon-back{
			position:relative;
			top:10px;
		}
		.g-footer-container {
		  position: absolute;
		  left: 0;
		  bottom: 0;
		  z-index:999;
		  width: 100%; 0 0 10px 0 hsla(0, 6%, 58%, 0.6);
        }
        .g-tabbar {
          display: flex;
          width: 100%;
          height: 50px;
          background-color: #fff;
        }
//sadvahdvadsadasdasasdsadsasa
        .g-tabbar .item {
            flex: 1;
            display:flex;
            flex-direction:column;
            justify-content:center;
            align-items:center;
        }
        //hhhhhh
        .g-tabbar .item:nth-of-type(3){
            flex: 2;
            background: #f60;
            color:#fff;
        }
        //hhhjjsiiioi
		  box-shadow:
		.g-tabbar .item:nth-of-type(4){
			flex: 2;
			background: #f00;
			color:#fff;
		}
		.g-tabbar  .iconfont {
			color:#333;
		    margin-bottom: 4px;
		    font-size:0.24rem;

		}
		.router-link-active{
		    color:#900;
	    }
	    .swiper{
	    	width:100%;
	    }
	    .swiper img{
	    	width: 100%;
	    }
	    .detail_decoration{
		    display: flex;
		    align-items: center;
		    height: 50px;
		    color: #fff;
		    background: linear-gradient(90deg,#ff7f4e,#ff3131);
		}
		.detail_decoration {
		    position: relative;
		    z-index: 5;
		}
		.detail_decoration .msg {
		    flex: 1;
		    font-size: 10px;
		}
		.detail_decoration .price {
		    margin: 0 10px;
		    font-size: 12px;
		    font-family: JDZH_Regular;
		}
		.detail_decoration .price em {
		    font-size: 26px;
		    font-family: JDZH_Bold;
		}
		.detail_decoration .countdown {
		    position: absolute;
		    right: 0;
		    top: 0;
		    width: 116px;
		    height: 100%;
		    text-align: center;
		    background-color: #f7f7f7;
		    display: flex;
		    flex-direction: column;
		    justify-content: center;
		}
		.detail_decoration .countdown .countdown_text {
		    margin-bottom: 2px;
		    font-size: 10px;
		    color: #333;
		}
		.detail_decoration .countdown .countdown_nums {
		    height: 18px;
		    font-size: 12px;
		    color: #e93b3d;
		}
		.detail_decoration .countdown .box {
		    display: inline-block;
		    margin: 0 3px;
		    width: 18px;
		    height: 18px;
		    background-size: 18px;
		    color: #e93b3d;
		    font-family: JDZH_Regular;
		}
		.fn_wrap .desc {
		    color: #e4393c;
		    padding: 5px 0 0;
		    line-height: 1.3;
		    position: relative;
		    font-size: 12px;
		    max-height: 60px;
		    overflow: hidden;
		}
		.fn_wrap, .shop_info_wrap {
		    padding: 15px 10px;
		    overflow: hidden;
		}
		.fn_wrap .desc a {
		    color: #e4393c;
		    text-decoration: underline;
		}
		.fn_wrap .fn {
		    position: relative;
		    color: #333;
		    overflow: hidden;
		    font-size: 16px;
		    font-weight: 400;
		    line-height: 18px;
		}
		.fn_wrap .fn .favour {
		    position: absolute;
		    right: 0;
		    top: 0;
		    display: inline-block;
		    padding-top: 26px;
		    margin-right: -10px;
		    line-height: 1em;
		    height: 10px;
		    width: 50px;
		    font-size: 10px;
		    color: #333;
		    text-align: center;
		}
</style>