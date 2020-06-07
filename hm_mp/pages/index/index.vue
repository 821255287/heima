<template>
	<view class="home">
		<swiper indicator-dots circular="true" interval="2000" autoplay>
			<swiper-item v-for="item in swiper" :key="item.id">
				<image :src="item.img" ></image>
			</swiper-item>
		</swiper>
		<!-- 导航区域 -->
		<view class="nav">
			
			<view class="nav_item" v-for="(item,index) in nav" :key="index" @click="navItemClick(item.path)">
				<view :class="item.icon"></view>
				<text>{{item.title}}</text>
					</view>
					
		</view>
		  
		<!-- 推荐商品区域 -->
		<view class="hot_goods">
			<view class="tit">推荐商品</view>
			<goodslists :goods= "goods" @goodsItemClick="goGoodsDetail"></goodslists>
		</view>
	</view>
</template>

<script>
	
	import goodslists from '../compoents/goods-list/goods-list.vue'

	export default {
		data() {
			return {
				swiper:[],
				goods:[],
				nav:[
				{
					icon:"iconfont icon-ziyuan",
					title:"黑马超市",
					path:'/pages/goods/goods'
				},
				{
					icon:"iconfont icon-guanyuwomen",
					title:"联系我们",
					path:'/pages/contact/contact'
				},
				{
					icon:"iconfont icon-tupian",
					title:"社区图片",
					path:'/pages/pics/pics'
				},
				{
					icon:"iconfont  icon-shipin",
					title:"学习视频",
					path:'/pages/videos/videos'
				}
				]
			}
		},
		components:{
			"goodslists":goodslists
		},
		onLoad() {
		this.getSwiper();
		this.getHotGoods()
		},
		methods: {
			async	getSwiper(){
				// 	console.log("获取轮播图的数据")
				
				//  const res = await uni.request({url:"http://localhost:8082/api/getlunbo"})								
				// 			// console.log(res)
				// if(res[1].data.status!==0) return uni.showToast({
				// 			title:"获取数据失败"
				// 		})
				// 				this.swiper = res[1].data.message
				const res = await this.$myRequest({
					url:"/api/getlunbo"
				})
			this.swiper = res.data.message
				
			},
			// 获取热门商品数据
		async getHotGoods(){
				const res  = await this.$myRequest({
					 url:'/api/getgoods?pageindex=1'
				})
			this.goods = res.data.message
			},
			// 导航点击的处理函数
			navItemClick(url){
				uni.navigateTo({
					url
				})
			},
			//跳转到商品详情页
			goGoodsDetail(id){
			console.log(id)
				uni.navigateTo({
					url:'../goods-detail/goods-detail?id='+id
				})
			}
			
		}					
	}
</script>

<style lang="scss">
	.home{
		swiper{
			width: 750rpx;
			height: 380rpx;
			image{
				width: 100%;
				height: 100%;
			}
		}
	}
	.nav{
		display: flex;
		.nav_item{
			// width: 25%;
			flex: 1;	
			// justify-content: center;
			// align-items: center;
			text-align: center;
			view{
				width: 120rpx;
				height: 120rpx;
				border-radius: 50%;
				background-color: #b50e03;
				margin: 20rpx auto;
				line-height: 120rpx;
				color: #fff;
				font-size: 50rpx;
			}
			.icon-tupian{
				font-size: 45rpx;
			}
			text{
				font-size: 30rpx;
			}
		}
	}
	.hot_goods{
		background-color: #eee;
		overflow: hidden;
		margin-top: 10px;
		.tit{
			height: 50px;
			line-height: 50px;
			color:$shop_Color;
			text-align: center;
			letter-spacing: 20rpx;
			background-color: #fff;
			margin: 7rpx 0;
		}
	
		
	}
</style>
