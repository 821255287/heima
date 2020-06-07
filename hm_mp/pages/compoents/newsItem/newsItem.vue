<template>
	<view>
		<view class="new_item" v-for="item in newsList" :key="item.id"
		@click="navigator(item.id)">
			<image :src="item.img_url"></image>
			<view class="right">
				<view class="title">
					{{item.title}}
				</view>
				
				<view class="info">
					<text>发表时间：{{item.add_time|formatDate}}</text>
					<text>浏览次数：{{item.click}}</text>
					
				</view>
			</view>
			
		</view>
	</view>
</template>

<script>
	export default {
		props:["newsList"],
		data() {
			return {
				
			}
		},
		methods: {
			navigator(id){ 
				
				this.$emit("itemClick",id)
			}
		},
		filters:{
				formatDate(date){
				
				const ndate = new Date(date)
				const year = ndate.getFullYear()
				const month = ndate.getMonth().toString().padStart(2,0)
				const day = ndate.getDay().toString().padStart(2,0)
				
				return year+"-"+month +"-"+day 
		}
	},
	}
</script>

<style lang="scss">
.new_item{
			display: flex;
			padding: 10rpx 20rpx;
			border-bottom: 1px solid $shop_Color;
			image{
				
				min-width: 200rpx;
				max-width: 200rpx;
				height: 150rpx;
			}
			.right{
				display: flex;
				flex-direction: column;
				justify-content: space-between;
				padding-left: 15rpx;
				.title{
					font-size: 30rpx;
					
				}
				.info{
					font-size: 24rpx;
					text:nth-child(2){
						margin-left: 30rpx;
						
					}
				}
			}
		}
</style>
