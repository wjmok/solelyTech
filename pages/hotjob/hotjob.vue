<template>
	<view>
		
		<view class="">
			
			<view class="jobList">
				<view class="item" v-for="(item,index) in caseData" :key="index" @click="Router.navigateTo({route:{path:'/pages/hotjobDetail/hotjobDetail'}})">
					<view class="flexRowBetween">
						<view class="tit fs13">网络推广/网络运营/网络优化SEO</view>
						<view class="pubColor">5k-6k</view>
					</view>
					<view class="flex lable color9">
						<view class="tt">西安 雁塔区</view>
						<view class="tt">经验不限</view>
						<view class="tt">学历不限</view>
					</view>
					<view class="flex mgt15 color9 fs12">
						<view class="photo"><image src="../../static/images/positionl-img.png" mode=""></image></view>
						<view>李希·招聘者</view>
					</view>
				</view>
			</view>
			
			<!-- 无数据 -->
			<view class="nodata"><image src="../../static/images/nodata.png" mode=""></image></view>
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
				is_show:false,
				caseData:[{},{},{},{}]
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
	/* @import "../../assets/style/navbar.css"; */
	page{background-color: #F5F5F5;}
	.jobList .item{margin-bottom: 20rpx;background: #fff;overflow: hidden;padding: 40rpx 2.666%;}
	.jobList .item .pic{width: 100%;height: 612rpx;}
	.jobList .item .tit{font-size: 28rpx;width: 80%;}
	.jobList .lable{margin-top: 20rpx;flex-wrap: wrap;}
	.jobList .lable .tt{font-size: 20rpx;line-height: 40rpx;padding: 0 20rpx;border-radius: 6rpx;background: #effeff;margin-right: 30rpx;}
	.jobList .photo{width: 56rpx;height: 56rpx;border-radius: 50%;overflow: hidden;margin-right: 20rpx;}
</style>
