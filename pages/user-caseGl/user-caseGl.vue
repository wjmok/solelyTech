<template>
	<view>
		
		<view class="caseGl mglr4">
			<view class="item flexRowBetween" v-for="(item,index) in caseData" :key="index" @click="Router.navigateTo({route:{path:'/pages/user-caseGlDetail/user-caseGlDetail'}})">
				<view class="infor">
					<view class="fs12 color9">项目编号：2020.04.15</view>
					<view class="flex row">
						<view class="icon"><image src="../../static/images/projectl-icon1.png" mode=""></image></view>
						<view><span class="mgr10 fs13 color6">合同编号：</span>1612547856</view>
					</view>
					<view class="flex row">
						<view class="icon"><image src="../../static/images/projectl-icon2.png" mode=""></image></view>
						<view><span class="mgr10 fs13 color6">项目名称：</span>百舌鸟小程序</view>
					</view>
					<view class="flex row">
						<view class="icon"><image src="../../static/images/projectl-icon7.png" mode=""></image></view>
						<view><span class="mgr10 fs13 color6">项目状态：</span>开发中</view>
					</view>
				</view>
				<view class="arrowR"><image src="../../static/images/0-icon.png" mode=""></image></view>
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
	page{padding-bottom: 60rpx;background-color: #F5F5F5;}	
	.caseGl .item{background-color: #fff;height: 280rpx;box-sizing: border-box;border-radius: 10rpx;overflow: hidden;margin-top: 30rpx;padding: 30rpx;}
	.caseGl .item .infor{width: 90%;}
	.caseGl .item .infor .icon{width: 34rpx;height: 34rpx;margin-right: 10rpx;}
	.caseGl .item .row{margin-top: 20rpx;}
</style>