<template>
	<view>
		
		<view class="goOut mglr4">
			<view class="item flexRowBetween" >
				<view class="fixIcon"><image src="../../static/images/to-go-outl-img.png" mode=""></image></view>
				<view class="infor" @click="Router.navigateTo({route:{path:'/pages//'}})">
					<view class="flex row"><span class="title">缘由：</span>出去见客户</view>
					<view class="flex row"><span class="title">起始时间：</span>2019.04.15 16:00</view>
					<view class="flex row"><span class="title">到达时间：</span>-------</view>
					<view class="flex row"><span class="title">返程时间：</span>-------</view>
					<view class="flex row"><span class="title">结束时间：</span>-------</view>
				</view>
				<view class="arriveBtn fs16 ftw"  @click="Router.navigateTo({route:{path:'/pages/staffUser-goOut-Arrive/staffUser-goOut-Arrive'}})">到达</view>
			</view>
			<view class="item flexRowBetween" >
				<view class="fixIcon"><image src="../../static/images/to-go-outl-img1.png" mode=""></image></view>
				<view class="infor" @click="Router.navigateTo({route:{path:'/pages/staffUser-goOutDetail/staffUser-goOutDetail'}})">
					<view class="flex row"><span class="title">缘由：</span>出去见客户</view>
					<view class="flex row"><span class="title">起始时间：</span>2019.04.15 16:00</view>
					<view class="flex row"><span class="title">到达时间：</span>2019.04.15 17:00</view>
					<view class="flex row"><span class="title">返程时间：</span>2019.04.15 18:00</view>
					<view class="flex row"><span class="title">结束时间：</span>2019.04.15 19:00</view>
				</view>
				<view class="arrowR"><image src="../../static/images/0-icon.png" mode=""></image></view>
			</view>
			<view class="item flexRowBetween" >
				<view class="fixIcon"><image src="../../static/images/to-go-outl-img.png" mode=""></image></view>
				<view class="infor" @click="Router.navigateTo({route:{path:'/pages/staffUser-goOutDetail/staffUser-goOutDetail'}})">
					<view class="flex row"><span class="title">缘由：</span>出去见客户</view>
					<view class="flex row"><span class="title">起始时间：</span>2019.04.15 16:00</view>
					<view class="flex row"><span class="title">到达时间：</span>2019.04.15 17:00</view>
					<view class="flex row"><span class="title">返程时间：</span>2019.04.15 18:00</view>
					<view class="flex row"><span class="title">结束时间：</span>2019.04.15 19:00</view>
				</view>
				<view class="arrowR"><image src="../../static/images/0-icon.png" mode=""></image></view>
			</view>
		</view>
		
		<view class="R-fixIcon"  @click="Router.navigateTo({route:{path:'/pages/staffUser-goOutMsg/staffUser-goOutMsg'}})"><image src="../../static/images/to-go-outl-icon.png" mode=""></image></view>
		
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
	
	.R-fixIcon{width: 110rpx;height: 110rpx;position: fixed;bottom:30%;right: 30rpx;z-index: 66;}
	
	.goOut .item{background-color: #fff;height: 364rpx;box-sizing: border-box;border-radius: 10rpx;overflow: hidden;margin-top: 30rpx;padding: 30rpx;position: relative;}
	.goOut .item .fixIcon{width: 70rpx;height: 64rpx;position: absolute;top: 0;right: 0;}
	.goOut .item .infor{width: 70%;}
	.goOut .item .row{margin-bottom: 26rpx;}
	.goOut .item .row:last-child{margin-bottom: 0;}
	.goOut .item .row .title{width: 160rpx;font-size: 26rpx;color: #666;}
	.arriveBtn{width: 180rpx;height: 76rpx;line-height: 76rpx;border-radius: 40rpx;text-align: center;color: #fff;background-image:linear-gradient(to bottom,#49e3de,#2995e1);}
</style>