<template>
	<view>
		<view class="goods_list">
			<view class="goods_item" v-for="item in goods" :key="item.id"
			@click="navitor(item.id)">
				<image :src="item.img_url"></image>
				<view class="price">
					<text>{{item.sell_price}}</text>
					<text>{{item.market_price}}</text>
				</view>
				<view class="name">{{item.title}}</view>
			</view>
		</view>
	</view>
</template>

<script>
	
	export default {
		props:["goods"],
		data() {
			return {
				
			}
		},
		methods: {
			navitor(id){
				this.$emit("goodsItemClick",id)
			}
		}
	}
</script>

<style lang="scss">
	.goods_list{
			display: flex;
			flex-wrap: wrap;
			justify-content: space-between;
			padding: 0 15rpx;
			.goods_item{
				background-color: #FFFFFF;
				width: 355rpx;
				margin: 10rpx 0;
				padding: 15rpx;
				box-sizing: border-box;
			image{
				display: block;
				margin: auto;
					width: 80%;
					height: 150px;							
				}
				.price{
					color: $shop_Color;
					font-size: 36rpx;
					padding-top: 15rpx;
					text:nth-child(2){
						color: #ccc;
						font-size: 28rpx;
						margin-left: 17rpx;
						text-decoration: line-through;
						
					}
					
					
				}
				.name{
					font-size: 28rpx;
					line-height: 50rpx;
					padding-bottom: 15rpx;
					padding-top: 10rpx;
				}
				
			}
		}
</style>
