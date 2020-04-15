<template>
	<view>
		
		<view class="orderNav flex whiteBj pdtb5">
			<view class="tt flexCenter">起始时间<image class="arrwB" src="../../static/images/to-promotel-icon.png" mode=""></image></view>
			<view class="tt flexCenter">截止时间<image class="arrwB" src="../../static/images/to-promotel-icon.png" mode=""></image></view>
		</view>
		<view class="mglr4">
			<view class="extension flex" v-for="(item,index) in extensionData" :key="index">
				<view class="photo"><image src="../../static/images/to-promotel-img.png" mode=""></image></view>
				<view>
					<view>涸鲋得水</view>
					<view class="mgt5 color6 fs13">2020-04-15</view>
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
				showView: false,
				score:'',
				wx_info:{},
				extensionData:3
			}
		},
		onLoad() {
			const self = this;
			//self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {

		},
	};
</script>

<style>
	@import "../../assets/style/orderNav.css";
	page{padding-bottom: 60rpx;background-color: #F5F5F5;}
	
	.extension{width: 100%;height: 160rpx;padding: 30rpx;box-sizing: border-box;border-radius: 10rpx;background-color: #fff;margin-top: 30rpx;}
	.extension .photo{width: 100rpx;height: 100rpx;border-radius: 50%;margin-right: 20rpx;}
</style>
