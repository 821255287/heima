<template>
	<view class="goods_list">
		<goodslist :goods="goods" @goodsItemClick="goGoodsDetail" ></goodslist>
		<view class="isOver" v-if="flag">-----我是有底线的-----</view>
	</view>
</template>

<script>
	import goodslist from '../compoents/goods-list/goods-list.vue'
	export default {
		data() {
			return {
				goods:[],
				pageindex:1,
				flag:false
			}
		},
		components:{
			goodslist
		},
		onLoad(){
			this.getHotGoods()
		},
		methods: {
			async getHotGoods(callback){
					const res  = await this.$myRequest({
						 url:'/api/getgoods?pageindex='+this.pageindex
					})
				this.goods = [...this.goods,...res.data.message]
				callback && callback()
				},
				//跳转到商品详情页
				goGoodsDetail(id){
				console.log(id)
					uni.navigateTo({
						url:'../goods-detail/goods-detail?id='+id
					})
				},
		},
		onReachBottom(){
			if(this.goods.length<this.pageindex*10) return this.flag = true
			this.pageindex++;
			this.getHotGoods()
		},
		onPullDownRefresh(){
			this.pageindex = 1;
			this.goods = []
			this.flag =false
			setTimeout(()=>{
				this.getHotGoods(()=>{
					uni.stopPullDownRefresh()
				})
			},500)
			
		},

	}
</script>

<style>
.goods_list{
	background-color: #ccc;
}
.isOver{
	width: 100%;
	height: 50px;
	line-height: 50px;
	text-align: center;
	font-size: 28rpx;
}
</style>
