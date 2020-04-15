<template>
	<view>
		
		<view class="">
			<view class="backBtn" @click="pre()">
				<image src="../../static/images/arrowL.png" mode=""></image>
			</view>
			<view class="mapBox">
				<image src="../../static/images/to-go-outl-img4.png" mode=""></image>
			</view>
			
			<view class="camera flexCenter">
				<view class="flexColumn">
					<view class="btn mgb10"><image src="../../static/images/to-go-outl-icon1.png" mode=""></image></view>
					<view>拍照</view>
				</view>
			</view>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				is_show: false,
				wx_info:{}
			}
		},
		onLoad() {
			const self = this;
			// self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
			pre(){
				this.$router.go(-1);
			},
			getMainData() {
				const self = this;
				console.log('852369')
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				self.$apis.orderGet(postData, callback);
			}
		}
	};
</script>

<style>
	page{height: 100%;background-color: #F5F5F5;box-sizing: border-box;}
	.backBtn{width: 20rpx;height: 36rpx;position: fixed;top: 70rpx;left: 28rpx; z-index: 10;}
	.mapBox{position: fixed;left: 0;top: 0;right: 0;bottom: 0; z-index: 1;}
	
	.camera{width: 100%;height: 300rpx;box-sizing: border-box;position: fixed;left: 0;right: 0;bottom: 0;z-index: 20;background-color: #fff;}
	.camera .btn{width: 212rpx;height: 142rpx;}
</style>