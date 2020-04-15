<template>
	<view>
		
		<view class="leaveList mglr4  fs13">
			<view class="item flexRowBetween" v-for="(item,index) in leaveData"  @click="Router.navigateTo({route:{path:'/pages/staffUser-leaveDetail/staffUser-leaveDetail'}})">
				<view class="infor">
					<view>申请时间：2020-04-15</view>
					<view class="mgt10">请假事由：朋友结婚</view>
				</view>
				<view class="rr fs12">
					<view class="pubColor mgb5 flexEnd">状态：人事审核</view>
					<view class="flexEnd"><image class="arrowR" src="../../static/images/0-icon.png" mode=""></image></view>
				</view>
			</view>
		</view>
		<view class="R-fixIcon"  @click="Router.navigateTo({route:{path:'/pages/staffUser-leaveAdd/staffUser-leaveAdd'}})"><image src="../../static/images/to-go-outl-icon.png" mode=""></image></view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				is_show: false,
				wx_info:{},
				leaveData:3
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
	
	.leaveList .item{background-color: #fff;height: 160rpx;box-sizing: border-box;border-radius: 10rpx;overflow: hidden;margin-top: 30rpx;padding:30rpx; align-items:flex-start;}
	.leaveList .item .infor{width: 55%;}
	.leaveList .item .rr{width: 45%;}
</style>