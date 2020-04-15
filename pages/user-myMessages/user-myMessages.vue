<template>
	<view>
		
		<view class=" mglr4 pdtb15">
			<textarea value="" placeholder="输入留言" placeholder-class="placeholder" />
		</view>
		<view class="f5H10"></view>
		
		<view class="submitbtn" style="padding: 150rpx 0 60rpx 0;">
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
				is_show:false
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
	@import "../../assets/style/editInfor.css";
	page{padding-bottom: 60rpx;}
	
	textarea{border: 0;height: 400rpx;}
	
</style>
