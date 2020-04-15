<template>
	<view>
		
		<view class="editLine pdlr4">
			<view class="item flexRowBetween">
				<view class="ll"><span class="red mgr5">*</span>您的姓名</view>
				<view class="rr">
					<textarea class="f5bj" value="" placeholder="" placeholder-class="placeholder" />
				</view>
			</view>
			<view class="item flexRowBetween">
				<view class="ll">请假类型</view>
				<view class="rr flex">
					<picker @change="seltResult" :value="index" :range="array">
						<view class="seltStyle flexRowBetween">
							<view class="">{{array[index]}}</view>
							<view style="width: 20rpx;height: 14rpx;"><image src="../../static/images/leave-icon.png" mode=""></image></view>
						</view>
					</picker>
					<!-- <input type="text" maxlength="11" value="" placeholder="请输入" placeholder-class="placeholder" /> -->
				</view>
			</view>
			<view class="item flexRowBetween">
				<view class="ll">起止时间</view>
				<view class="rr flexRowBetween" style="flex-wrap: wrap;">
					<view class="seltTime">
						<view class="flexRowBetween">
							<view></view>
							<view class="arrowB"><image src="../../static/images/leave-icon.png" mode=""></image></view>
						</view>
					</view>
					<view class="seltTime">
						<view class="flexRowBetween">
							<view></view>
							<view class="arrowB"><image src="../../static/images/leave-icon.png" mode=""></image></view>
						</view>
					</view>
					<view class="seltTime">
						<view class="flexRowBetween">
							<view></view>
							<view class="arrowB"><image src="../../static/images/leave-icon.png" mode=""></image></view>
						</view>
					</view>
					<view class="seltTime">
						<view class="flexRowBetween">
							<view></view>
							<view class="arrowB"><image src="../../static/images/leave-icon.png" mode=""></image></view>
						</view>
					</view>
				</view>
			</view>
		</view>
		
		<view class="submitbtn" style="padding-top: 200rpx;">
			<view class="btn">提交</view>
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
	
	.seltTime{width: 48%;height: 60rpx;border: 1px solid #eee;padding: 0 20rpx;box-sizing: border-box;margin-bottom: 30rpx;}
	.seltTime>view{width: 100%;height: 100%;}
	.arrowB{width: 20rpx;height: 14rpx;}
</style>
