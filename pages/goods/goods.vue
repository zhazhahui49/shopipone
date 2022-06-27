<template>
	<view>
		<goods-list :goods="goods" @goodsItemClick="goGoodsDetail"></goods-list>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				goods: [],
				pagenum: 1

			}
		},
		onLoad() {
			this.getgoods()
		},
		onReachBottom() {
			this.pagenum++
			this.getgoods()

		},
		onPullDownRefresh() {
			this.pagenum = 1;
			this.goods = []
			this.getgoods(() => {
				uni.stopPullDownRefresh()
			})

		},
		methods: {
			getgoods(callBack) {
				this.$myRequest({
					url: '/goods/search?pagenum=' + this.pagenum
				}).then(res => {
					this.goods = [...this.goods, ...res.data.message.goods]
					callBack && callBack()
				})

			},
			goGoodsDetail(id){
				uni.navigateTo({
					url:'/pages/goods-detail/goods-detail?id='+id
				})
			}

		}
	}
</script>

<style>

</style>
