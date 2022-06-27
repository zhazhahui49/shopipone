<template>
 	<view class="pics">
 		<scroll-view class="left " scroll-y>
 			<view :class="active===index?'active':''" @click="active1(index)" v-for="(item,index) in mig" :key="index">
 				{{item.cat_name}}</view>
				 
 		</scroll-view>
 	</view>
 </template>

 <script>
 	export default {
 		data() {
 			return {
 				mig: [],
 				active: 0,

 			}
 		},
 		onLoad() {
 			this.getPicsCate()
 		},
 		methods: {
 			getPicsCate() {
 				this.$myRequest({
 					url: "/categories"
 				}).then((res) => {
 					this.mig = res.data.message
 				})
 			},
 			active1(index) {
 				this.active = index
 			}

 		}
 	}
 </script>

 <style lang="scss" scoped>
 	page {
 		height: 100%;
 	}

 	.pics {
 		height: 100%;
 		display: flex;

 		.left {
 			width: 200rpx;
 			height: 100%;
 			border-right: 1px solid #eee;

 			view {
 				height: 60px;
 				line-height: 60px;
 				color: #333;
 				text-align: center;
 				font-size: 30rpx;
 				border-top: 1px solid #eee;
 			}

 			.active {
 				background: $shop-color;
 				color: #fff;
 			}
 		}

 		.right {
 			height: 100%;
 			width: 520rpx;
 			margin: 10rpx auto;

 			.item {
 				image {
 					width: 520rpx;
 					height: 520rpx;
 					border-radius: 5px;
 				}

 				text {
 					font-size: 30rpx;
 					line-height: 60rpx;
 				}
 			}
 		}
 	}
 </style>
