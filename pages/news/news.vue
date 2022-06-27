<template>
	<view>
		<news-item :list="newlist"></news-item>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				newlist:[]
			}
		},
		onLoad(){
			this.getNews()
		},
		methods: {
			getNews(){
				this.$myRequest({
					url:"/goods/detail?goods_id=8888"
				}).then((res)=>{
					//console.log(res.data.message.goods_id)
					this.newlist=res.data
					console.log(this.newlist)
				})
			}
			
			
		}
	}
</script>

<style>

</style>
