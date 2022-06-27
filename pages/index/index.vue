<template>
	<view class="home">
		<swiper indicator-dots circular>
			<swiper-item v-for="item in swiper" :key="item.goods_id">
				<image :src="item.image_src" mode=""></image>
			</swiper-item>
		</swiper>
		<view class="nav">
			<view class="nav_item" v-for="(item,index) in navs" :key="index" @click="navItemClick(item.path)">
				<view :class="item.icon"></view>
				<text>{{item.title}}</text>
			</view>
		</view>
		
				<view class="hot_goods">
					<view class="tit">推荐商品</view>
					<goods-list @goodsItemClick="goGoodsDetail" :goods="goods"></goods-list>
				</view>
	</view>
</template>

<script>
	import goodsList from '../../components/goods-list/goods-list.vue'
	export default {
		data() {

			return {
				title: 'Hello',
				swiper: [],
				goods:[],
				navs: [{
						icon: 'iconfont icon-ziyuan',
						title: '黑马超市',
						path: '/pages/goods/goods'
					},
					{
						icon: 'iconfont icon-guanyuwomen',
						title: '联系我们',
						path: '/pages/contact/contact'
					},
					{
						icon: 'iconfont icon-tupian',
						title: '社区图片',
						path: '/pages/pics/pics'
					},
					{
						icon: 'iconfont icon-shipin',
						title: '学习视频',
						path: '/pages/videos/videos'
					}
				]
			}
		},
		onLoad() {
			this.getSwipers();
			this.getgoods()
		},
		methods: {
			async getSwipers() {
				// console.log("===")
				// uni.request({
				// 	url: "https://api-hmugo-web.itheima.net/api/public/v1/home/swiperdata",
				// 	success: (res) => {

				// 		if (res.data.meta.status != 200) {

				// 			return
				// 		}
				// 		this.swiper=res.data.message
				// 	}
				// })
				const res = await this.$myRequest({
					url: "/home/swiperdata"
				}).then(res => {
					this.swiper = res.data.message
				})
			},
			getgoods(){
				this.$myRequest({
					url:'/goods/search'
				}).then(res=>{
					this.goods=res.data.message.goods
				})
			},
			navItemClick(url){
				uni.navigateTo({
					url
				})
			},
			goGoodsDetail(id){
				uni.navigateTo({
					url:'/pages/goods-detail/goods-detail?id='+id
					
				})
			}
		},
	}
</script>

<style lang="scss">
	.home {

		swiper-item {
			width: 750rpx;
			height: 380rpx;

			image {
				width: 100%;
				height: 100%;
			}
		}

		.nav {
			display: flex;

			.nav_item {
				flex: 1;
				text-align: center;

				view {
					width: 120rpx;
					height: 120rpx;
					background: #b50e03;
					border-radius: 60rpx;
					margin: 10px auto;
					line-height: 120rpx;
					color: #fff;
					font-size: 50rpx;
				}

				.icon-tupian {
					font-size: 45rpx;
				}

				text {
					font-size: 30rpx;
				}
			}
		}
				.hot_goods {
					background: #eee;
					overflow: hidden;
					margin-top: 10px;
					.tit{
						height: 50px;
						line-height: 50px;
						color: #b50e03;
						text-align: center;
						letter-spacing: 20px;
						background: #fff;
						margin: 7rpx 0;
					}
				}

	}

	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.logo {
		height: 200rpx;
		width: 200rpx;
		margin-top: 200rpx;
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 50rpx;
	}

	.text-area {
		display: flex;
		justify-content: center;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}
</style>
