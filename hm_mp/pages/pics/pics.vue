<template>
	<view class="pics">
		<scroll-view class="left" scroll-y>
			<view v-for="(item,index) in cates" :key="item.id"
			:class="idx===index?'active':''" @click="btn(index,item.id)">
				{{item.title}}
			</view>			
		</scroll-view>
		<scroll-view class="right" scroll-y>
			<view class="item" v-for="items in secondData" :key="items.id">
				<image :src="items.img_url" @click="preview(items.img_url)"></image>
				<text>{{items.title}}</text>
			</view>
			<view v-if="secondData.length===0">暂无数据</view>
		</scroll-view>
	</view>
</template>
 
<script>
	export default {
		data() {
			return {
				cates:[],
				idx:0,
				secondData:[]
			}
		},
		methods: {
		async	getPicsCate(){
			const res = await this.$myRequest({
					url:"/api/getimgcategory"
				})
				this.cates = res.data.message
			},
		async btn(index,id){
				this.idx = index
				// console.log(id)
				const res = await this.$myRequest({
					url:'/api/getimages/'+id
				})
				this.secondData = res.data.message
				// console.log(this.secondData)
			},
			preview(current){
				
				const urls = this.secondData.map(item=>{
					return item.img_url
				})
				console.log(urls)
				uni.previewImage({
					current,
					urls
				})
			}
		},
		onLoad(){
			this.getPicsCate()
		}
	}
</script>

<style lang="scss">
	page{
		height: 100%;
	}
	.pics{
		display: flex;
		height: 100%;
		// height: 100vh;
		.left{
			width: 200rpx;
			height: 100%;
			border-right: 1px solid #eee;
			view{
				height: 60px;
				line-height: 60px;
				color: #333;
				text-align: center;
				font-size: 30rpx;
				border-top: 1px solid #eee;								
			}
		}
		
		.active{
			background-color: $shop_Color;
			color: #fff;
		}
		.right{
				height: 100%;
				width: 520rpx;
				margin: 10rpx auto;
				.item{
					image{
						width: 520rpx;
						height: 520rpx;
						border-radius: 5px;
						margin-top: 10rpx;
					}
					text{
						font-size: 30rpx;
						line-height: 60rpx;
					}
				}
				
		}
		
	}

</style>
