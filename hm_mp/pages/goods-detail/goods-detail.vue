<template>
	<view class="goods_detail">
		<swiper indicator-dots interval="3000" circular autoplay="true">
			<swiper-item v-for="(item,index) in swiper" :key="index">
				<image :src="item.src"></image>
			</swiper-item>
		</swiper>
		
		<view class="box1">
			<view class="price">
				<text>{{Info.sell_price}}</text>
				<text>{{Info.market_price}}</text>
			</view>
			<view class="goods_name">{{Info.title}}</view>
			
			<view class="box2">
				<view>货号:{{Info.goods_no}}</view>
				<view>货存:{{Info.stock_quantity}}</view>
			</view>
			
			<view class="box3">
				<view class="title">	详情介绍	</view>
				<view class="content" >
					<rich-text :nodes="content"></rich-text>
				</view>
			</view>
		</view>
		<view class="goods_nav">
			<uni-goods-nav :fill="true"  :options="options" :buttonGroup="buttonGroup"  @click="onClick" @buttonClick="buttonClick" />
		</view>
		
	</view>
</template>

<script>
	import uniGoodsNav from '@/components/uni-goods-nav/uni-goods-nav.vue'
	export default {
		data() {
			
			return {
				id:0,
				swiper:[],
				Info:{},
				content:"",
				 options: [{
				            icon: 'headphones',
				            text: '客服'
				        }, {
				            icon: 'shop',
				            text: '店铺',
				            info: 2,
				            infoBackgroundColor:'#007aff',
				            infoColor:"red"
				        }, {
				            icon: 'cart',
				            text: '购物车',
				            info: 2
				        }],
				        buttonGroup: [{
				          text: '加入购物车',
				          backgroundColor: '#ff0000',
				          color: '#fff'
				        },
				        {
				          text: '立即购买',
				          backgroundColor: '#ffa200',
				          color: '#fff'
				        }
				        ]
			}
		},
		methods: {
			async getSwipers(){
				const res = await this.$myRequest({
					url:'/api/getthumimages/'+this.id
				})
				// console.log(res)
				this.swiper =res.data.message
			},
			async getDetailInfo(){
				const res = await this.$myRequest({
					url:"/api/goods/getinfo/"+this.id
				})
				this.Info = res.data.message[0]
				// console.log(this.Info)
			},
			async getDetailContent(){
				const res = await this.$myRequest({
					url:"/api/goods/getdesc/"+this.id
				})
			
				this.content = res.data.message[0].content
					// console.log(this.content)
			},
			onClick (e) {
			       uni.showToast({
			         title: `点击${e.content.text}`,
			         icon: 'none'
			       })
			     },
			     buttonClick (e) {
			       console.log(e)
			       this.options[2].info++;
			     }
			   
		},
		onLoad(option){
			// console.log(option)
			this.id = option.id
			this.getSwipers();
			this.getDetailInfo();
			this.getDetailContent();
		},
		  components: {uniGoodsNav},
		  
	}
</script>

<style lang="scss">
	.goods_detail{
		swiper{
			height: 700rpx;
			image{
				width: 100%;
				height: 100%;
			}
		}
	}
.box1{
	padding: 10px;
	.price{
		font-size: 35rpx;
		color: $shop_Color;
		line-height: 80rpx;
		text:nth-child(2){
			color: #CCCCCC;
			font-size: 28rpx;
			text-decoration: line-through;
			margin-left: 20rpx;
			
		}
	}
	.goods_name{
		font-size: 32rpx;
		line-height: 60rpx;
	}
	.goods_name::after{
		content: "";
		border-bottom: 5px solid #eee;
		display: block;
		width: 750rpx;
	}
	.box2{
		padding: 0 10px;
		font-size: 32rpx;
		line-height: 70rpx;
	
	}
	.box2::after{
		content: "";
		border-bottom: 5px solid #eee;
		display: block;
		width: 750rpx;
		
	}
	.box3{
		padding-bottom: 50px;
		.title{
			font-size: 32rpx;
			padding-left: 10px;
			border-bottom: 1px solid #eee;
			line-height: 70rpx;
		}
		.content{
			padding: 10px;
			font-size: 28rpx;
			color: #333;
			line-height: 50rpx;
		}
	}
	
 .goods_nav{
		height: 50px;
		width: 100%;
		position: fixed !important;
		bottom: 0 !important;
		left: 0 !important;
		z-index: 44 !important;
	}

}
</style>
