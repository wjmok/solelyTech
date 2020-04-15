<template>
	<view>
		
		<view class="flexColumn" style="padding-top: 100rpx;padding-bottom: 80rpx;">
			<view class="photo"><image src="../../static/images/the-loginl-img.png" mode=""></image></view>
			<view class="fs15 ftw mgt10">米桃子</view>
		</view>
		<!-- <view class="loginBj pr">
			<image src="../../static/images/the-login-img.png" mode=""></image>
		</view> -->
		
		<view class="loginCont">
			<view class="item flex mgb20">
				<view class="icon"><image src="../../static/images/the-loginl-icon.png" mode=""></image></view>
				<view class="input">
					<input type="text" value="" placeholder="Secitong" placeholder-class="placeholder">
				</view>
			</view>
			<view class="item flex mgb20">
				<view class="icon"><image src="../../static/images/the-loginl-icon1.png" mode=""></image></view>
				<view class="input">
					<input type="password" value="" placeholder="请输入您的密码" placeholder-class="placeholder">
				</view>
			</view>
			
			<view class="item submitbtn" style="padding:200rpx 0 0 0;border: 0;" >
				<button class="Wbtn" type="submint" @click="Router.navigateTo({route:{path:'/pages/staffUser/staffUser'}})">登录</button>
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
	.loginBj{width: 440rpx;height: 440rpx;margin: 0 auto;}
	.loginBj image{width: 100%;height: 100%;}
	
	.photo{width: 160rpx;height: 160rpx;border-radius: 50%;overflow: hidden;}
	
	.loginCont{width:90%;margin: 0 auto;z-index: 2;background: #fff;padding: 0rpx 60rpx;box-sizing: border-box;}
	.loginCont .item{height: 80rpx;box-sizing: border-box;padding: 0 20rpx;border-bottom: 1px solid #c3c3c3;}
	.loginCont .item .icon{width: 36rpx;height: 36rpx;margin-right: 30rpx;}
	.loginCont .item .input{width: 85%;}
	.loginCont .item .input input{font-size: 26rpx;height: 60rpx;}
</style>
