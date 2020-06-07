<template>
	<view class="contact">
		<image src="" class="img"></image>
		<view class="info">
			<view @click="phone">联系电话:159865742</view>
			<view>联系地址:广东省深圳市龙岗区坂田街道</view>
		</view>
		<map class="map" :longitude="longitude" :latitude="latitude"
		:markers="markers" :scale="scale"></map>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				longitude:114.066967,
				latitude:22.632075,
				scale:13,
				markers:[
					{
						longitude:114.066967,
						latitude:22.632075,
						iconPath:"../../static/hmlogo.png",
						width:30,
						height:30
					}
				]
			}
		},
		methods: {
			phone(){
				console.log("ee")
				uni.makePhoneCall({
					phoneNumber:"15919350405"
				})
			}
		}
	}
</script>

<style lang="scss">
.contact{	
	.img{
		width: 750rpx;
		height: 320rpx;
	}
	.info{
		padding: 10px 20px;
		view{
			line-height: 80rpx;
			border-bottom: 1px solid #eee;
		}
	}
}
.map{
	width: 750rpx;
	height: 750rpx;
}
</style>
