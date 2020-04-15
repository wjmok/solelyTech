<template>
	<view>
		
		<view class="mglr4 pdtb15">
			<view class="fs15 ftw">起始</view>
			<view class="flex mgt10">
				<view class="mgr25 fs13 color6">时间</view>
				<view>2020-4-15 16:30</view>
			</view>
			<view class="flex mgt10">
				<view class="mgr25 fs13 color6">缘由</view>
				<view>见客户</view>
			</view>
		</view>
		<view class="f5H5"></view>
		<view class="mglr4 pdtb15">
			<view class="fs15 ftw">到达</view>
			<view class="flex mgt10">
				<view class="mgr25 fs13 color6">时间</view>
				<view>2020-4-15 17:00</view>
			</view>
			<view class="flex picLis">
				<view class="tt"><image src="../../static/images/to-go-outl-img3.png" mode=""></image></view>
				<view class="tt"><image src="../../static/images/to-go-outl-img5.png" mode=""></image></view>
			</view>
		</view>
		<view class="f5H5"></view>
		<view class="mglr4 pdtb15">
			<view class="fs15 ftw">返程</view>
			<view class="flex mgt10">
				<view class="mgr25 fs13 color6">时间</view>
				<view>2020-4-15 18:00</view>
			</view>
			<view class="flex picLis">
				<view class="tt"><image src="../../static/images/to-go-outl-img3.png" mode=""></image></view>
			</view>
		</view>
		<view class="f5H5"></view>
		<view class="mglr4 pdtb15">
			<view class="fs15 ftw">结束</view>
			<view class="flex mgt10">
				<view class="mgr25 fs13 color6">时间</view>
				<view>2020-4-15 18:30</view>
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
				wx_info:{},
				caseData:3
			}
		},
		onLoad() {
			const self = this;
			// self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
			
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
	page{padding-bottom: 60rpx;}
	.picLis{flex-wrap: wrap;}
	.picLis .tt{width: 300rpx;height: 200rpx;margin:20rpx 30rpx 0 0;}
	
	
</style>