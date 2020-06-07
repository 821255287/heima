<template>
	<view class="news_detail">
		<text class="title">{{contents.title}}</text>
		<view class="info">
			<text>发表时间:{{contents.add_time|formatDate}}</text>
			<text>浏览次数:{{contents.click}}</text>
		</view>
		<view class="content" >
			<rich-text :nodes="contents.content"></rich-text>
		</view>
		
	
	</view>
</template>

<script>
	export default {
		data() {
			return {
				id:0,
				contents:[]
			}
		},
		methods: {
			async getNewsDetail(){
			const res = await this.$myRequest({
					url:"/api/getnew/"+this.id,
					
				})
				
				// console.log(res.data.message)
				this.contents = res.data.message[0]
				console.log(this.contents)
			}
		},
		onLoad(option){
			this.id = option.id
			this.getNewsDetail()
		}
	}
</script>

<style lang="scss">
.news_detail{
	font-size: 30rpx;
	padding: 0 20rpx;
	.title{
		text-align: center;
		width: 710rpx;
		display: block; 
		margin:  20rpx 0;
		
	}
	.info{
		display: flex;
		justify-content: space-between;
	}
	}
</style>
