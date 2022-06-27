<template>
	<view class="contact">
		<image class="img" src="http://www.itcast.cn/2018czydz/images/gywmban.jpg"></image>
		<view class="info">
			<view @click="phone">联系电话：4008-517-517 ( 点击拨打 )</view>
			<view>XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX</view>
		</view>
		<map class="map" :longitude="longitude" :scale="scale" :latitude="latitude" :markers="markers"></map>
	</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				longitude: 116.404269,
				latitude: 39.916485,
				scale: 13,
				markers: [{
					longitude: 116.404269,
					latitude: 39.916485,

					width: 30,
					height: 30
				}]

			}
		},
		methods: {
			 phone()  {
				uni.makePhoneCall({
					phoneNumber: '4008-517-517'
				})
			}

		}
	}
</script>

<style lang="scss" scoped>
	.contact {
		.img {
			width: 750rpx;
			height: 320rpx;
		}

		.info {
			padding: 10rpx 20rpx;
			font-size: 30rpx;

			view {
				line-height: 80rpx;
				border-bottom: 1px solid #eee;
			}
		}

		.map {
			width: 750rpx;
			height: 750rpx;
		}
	}
</style>
