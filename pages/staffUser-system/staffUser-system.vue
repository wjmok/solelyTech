<template>
	<view>
		
		<view class="system flexRowBetween mglr4">
			<view class="item flex" @click="Router.navigateTo({route:{path:'/pages/staffUser-systemDetail/staffUser-systemDetail'}})">
				<view class="icon"><image src="../../static/images/provisionsl-icon.png" mode=""></image></view>
				<view class="tit">外出制度</view>
			</view>
			<view class="item flex" @click="Router.navigateTo({route:{path:'/pages/staffUser-systemDetail/staffUser-systemDetail'}})">
				<view class="icon"><image src="../../static/images/provisionsl-icon1.png" mode=""></image></view>
				<view class="tit">薪资制度</view>
			</view>
			<view class="item flex" @click="Router.navigateTo({route:{path:'/pages/staffUser-systemDetail/staffUser-systemDetail'}})">
				<view class="icon"><image src="../../static/images/provisionsl-icon2.png" mode=""></image></view>
				<view class="tit">年假制度</view>
			</view>
			<view class="item flex" @click="Router.navigateTo({route:{path:'/pages/staffUser-systemDetail/staffUser-systemDetail'}})">
				<view class="icon"><image src="../../static/images/provisionsl-icon3.png" mode=""></image></view>
				<view class="tit">日志制度</view>
			</view>
			<view class="item flex" @click="Router.navigateTo({route:{path:'/pages/staffUser-systemDetail/staffUser-systemDetail'}})">
				<view class="icon"><image src="../../static/images/provisionsl-icon4.png" mode=""></image></view>
				<view class="tit">请假制度</view>
			</view>
			<view class="item flex" @click="Router.navigateTo({route:{path:'/pages/staffUser-systemDetail/staffUser-systemDetail'}})">
				<view class="icon"><image src="../../static/images/provisionsl-icon5.png" mode=""></image></view>
				<view class="tit">迟到制度</view>
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
				wx_info:{}
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
	page{padding-bottom: 60rpx;}
	.system{flex-wrap: wrap;}
	.system .item{width: 345rpx;height: 160rpx;box-shadow: 0 0 12rpx rgba(0,0,0,0.1);box-sizing: border-box;padding: 30rpx 40rpx;margin-top: 30rpx;}
	.system .item .icon{width: 108rpx;height: 109rpx;margin-right: 20rpx;}
</style>
