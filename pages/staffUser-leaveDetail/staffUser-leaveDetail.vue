<template>
	<view>
		
		<view class="editLine pdlr4">
			<view class="item flexRowBetween">
				<view class="ll"><span class="red mgr5">*</span>您的姓名</view>
				<view class="rr">
					<textarea class="f5bj" value="人事架构看如果国家开发的理解就过了几个放大了科技股份看到两个" placeholder="" disabled placeholder-class="placeholder" />
				</view>
			</view>
			<view class="item flexRowBetween">
				<view class="ll">请假类型</view>
				<view class="rr flex">
					<!-- <picker @change="seltResult" :value="index" :range="array"> -->
						<view class="seltStyle flexRowBetween">
							<view class="">事假</view>
							<!-- <view style="width: 20rpx;height: 14rpx;"><image src="../../static/images/leave-icon.png" mode=""></image></view> -->
						</view>
					<!-- </picker> -->
				</view>
			</view>
			<view class="item flexRowBetween">
				<view class="ll">起止时间</view>
				<view class="rr">
					<view class="seltTime">
						<view class="input">2020-04-15 09:00</view>
					</view>
					<view class="seltTime mgt15">
						<view class="input">2020-04-15 18:30</view>
					</view>
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
				is_show:false,
				array: ['','病假','事假','婚假'],
				index: 0
			}
		},
		onLoad() {
			const self = this;
			// self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
			seltResult(e) {
				console.log('picker发送选择改变，携带值为', e.target.value)
				this.index = e.target.value
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
	@import "../../assets/style/editInfor.css";
	page{padding-bottom: 60rpx;}
	
	.editLine .item{border-bottom: 0;padding: 30rpx 0;}
	.editLine .item .rr{color: #666;font-size: 26rpx;}
	.editLine .item textarea{height: 260rpx;box-sizing: border-box;}
	.seltStyle{width: 340rpx;height: 60rpx;border: 1px solid #eee;padding: 0 20rpx;box-sizing: border-box;}
	
	.seltTime{width: 340rpx;height: 60rpx;border: 1px solid #eee;padding: 0 20rpx;box-sizing: border-box;margin-bottom: 30rpx;}
</style>
