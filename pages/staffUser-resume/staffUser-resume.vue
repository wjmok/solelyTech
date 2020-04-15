<template>
	<view>
		
		<view class="resume">
			<view class="item flex" v-for="(item,index) in resumeData" :key="index" @click="Router.navigateTo({route:{path:'/pages/staffUser-resumeDetail/staffUser-resumeDetail'}})">
				<view class="photo"><image src="../../static/images/resume-managementl-img.png" mode=""></image></view>
				<view class="infor">
					<view class="tit">林晓梅</view>
					<view class="flex pdtb5">
						<view class="flex lable">
							<view class="icon"><image src="../../static/images/resume-managementl-icon.png" mode=""></image></view>
							<view>西安</view>
						</view>
						<view class="flex lable">
							<view class="icon"><image src="../../static/images/resume-managementl-icon2.png" mode=""></image></view>
							<view>女</view>
						</view>
						<view class="flex lable">
							<view class="icon"><image src="../../static/images/resume-managementl-icon3.png" mode=""></image></view>
							<view>大专</view>
						</view>
						<view class="flex lable">
							<view class="icon"><image src="../../static/images/resume-managementl-icon4.png" mode=""></image></view>
							<view>1-3年</view>
						</view>
					</view>
					<view class="fs12 color6">应聘职位：网络推广</view>
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
				wx_info:{},
				resumeData:3
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
	.resume .item{background-color: #fff;height: 220rpx;box-sizing: border-box;overflow: hidden;border-bottom: 20rpx solid #F5F5F5;padding: 30rpx 20rpx;}
	.resume .item .photo{width: 120rpx;height: 120rpx;border-radius: 50%;margin-right: 20rpx;}
	.resume .item .infor{width: 79%;}
	.resume .item .infor .icon{width: 24rpx;height: 24rpx;margin-right: 10rpx;}
	.resume .item .lable{margin-right: 36rpx;font-size: 24rpx; color: #666;}
	
</style>