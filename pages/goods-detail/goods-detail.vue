<template>
	<view class="goods_detail">
		<swiper>
			<swiper-item v-for="(time,index) in swipers " :key="index">
				<image :src="time"></image>
			</swiper-item>
		</swiper>
		<view class="box1">
			<view class="price">
				<text>￥{{goodsData.goods_price}}</text>
				<text>￥{{goodsData.goods_price}}</text>
			</view>
			<view class="goods_name">{{goodsData.goods_name}}</view>
		</view>
		<view class="line"></view>
		<view class="box2">
			<view>货号：{{goodsData.add_time}}</view>
			<view>库存：{{goodsData.cat_one_id}}</view>
		</view>
		<view class="line"></view>
		<view class="box3">
			<view class="tit">商品详情：</view>
			<view class="contact">
				<rich-text :nodes="goodsData.goods_introduce"></rich-text>
			</view>
		</view>
		<uni-goods-nav class="goods_nav" :fill="true" :options="options" :buttonGroup="buttonGroup" @click="onClick"
			@buttonClick="buttonClick" />
	</view>
</template>

<script>
	export default {
		data() {
			return {
				id: 0,
				swipers: [],
				goodsData: {},
				options: [{
					icon: 'headphones',
					text: '客服'
				}, {
					icon: 'shop',
					text: '店铺',
					info: 2,
					infoBackgroundColor: '#007aff',
					infoColor: "red"
				}, {
					icon: 'cart',
					text: '购物车',
					info: 2
				}],
				buttonGroup: [{
						text: '加入购物车',
						backgroundColor: '#ff0000',
						color: '#fff'
					},
					{
						text: '立即购买',
						backgroundColor: '#ffa200',
						color: '#fff'
					}
				]
			}
		},
		methods: {
			getSwipers() {
				this.$myRequest({
					url: '/goods/detail?goods_id=' + this.id
				}).then(res => {
					this.swipers = [res.data.message.goods_big_logo, res.data.message.goods_small_logo]
					// console.log(this.swipers)
				})
			},
			getDetail() {
				this.$myRequest({
					url: '/goods/detail?goods_id=' + this.id
				}).then(res => {
					this.goodsData = res.data.message
					console.log(this.goodsData)
				})
			}
		},
		onLoad(options) {
			this.id = options.id
			this.getSwipers()
			this.getDetail()
		}
	}
</script>

<style lang="scss">
	.goods_detail {
		swiper {
			height: 700rpx;

			image {
				width: 100%;
				height: 100%;
			}
		}

		.box1 {
			padding: 10px;

			.price {
				font-size: 35rpx;
				color: $shop-color;
				line-height: 80rpx;

				text:nth-child(2) {
					color: #ccc;
					font-size: 28rpx;
					text-decoration: line-through;
					margin-left: 20rpx;
				}
			}

			.goods_name {
				font-size: 32rpx;
				line-height: 60rpx;
			}
		}

		.box2 {
			padding: 0 10px;
			font-size: 32rpx;
			line-height: 70rpx;
		}

		.box3 {
			padding-bottom: 50px;

			.tit {
				font-size: 32rpx;
				padding-left: 10px;
				border-bottom: 1px solid #eee;
				line-height: 70rpx;
			}

			.content {
				padding: 10px;
				font-size: 28rpx;
				color: #333;
				line-height: 50rpx;
			}
		}
	}

	.goods_nav {
		position: fixed;
		bottom: 0;
		width: 100%;
	}

	.line {
		height: 10rpx;
		width: 750rpx;
		background: #eee;
	}
</style>
