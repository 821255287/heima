<template>
	<view class="news">
	<newitem :newsList="newsList" @itemClick="goDetail"></newitem>
	
	</view>
</template>

<script>
	import newitem from '../compoents/newsItem/newsItem.vue'
	export default {
		data() {
			return {
				newsList:[] 
			}
		},
		components:{ 
			newitem
		},
		methods: {
		 async	getNews(){
			const res = await	this.$myRequest({
					url:'/api/getnewslist'
				})
				this.newsList = res.data.message
			},
			goDetail(id){
				console.log(id)
				uni.navigateTo({
					url:"../news-detail/news-detail?id="+id
				})
			}
		},
		onLoad(){
			this.getNews()
		}
	}
</script>

<style lang="scss">
	.news{
		
	}

</style>
