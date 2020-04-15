<template>
	<view>
		
		<view class="flexCenter" style="padding-top: 136rpx;padding-bottom:160rpx;">
			<view class="bigIcon"><image src="../../static/images/projectl-icon.png" mode=""></image></view>
		</view>
		
		<view class="loginCont">
			<view class="item flex mgb25">
				<view class="icon"><image src="../../static/images/the-loginl-icon1.png" mode=""></image></view>
				<view class="input">
					<input type="password" maxlength="11" value="" placeholder="输入绑定手机号" placeholder-class="placeholder">
				</view>
			</view>
			
			<view class="item submitbtn" style="padding:0;border: 0;" @click="Router.navigateTo({route:{path:'/pages/user-caseGl/user-caseGl'}})">
				<button class="Wbtn" type="submint">确定</button>
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
				wx_info:{}
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
	.bigIcon{width: 174rpx;height:222rpx;margin: 0 auto;}
	
	.loginCont{width:90%;margin: 0 auto;z-index: 2;background: #fff;padding: 0rpx 60rpx;box-sizing: border-box;}
	.loginCont .item{height: 80rpx;box-sizing: border-box;padding: 0 30rpx;border: 1px solid #c3c3c3;border-radius: 10rpx;}
	/* .loginCont .item .icon{width: 36rpx;height: 36rpx;margin-right: 30rpx;} */
	.loginCont .item .input{width: 100%;}
	.loginCont .item .input input{font-size: 26rpx;height: 60rpx;text-align: center;}
</style>
