<template>
	<view>
		<view class="userHead pr">
			<view class="headbj"><image src="../../static/images/about-img.png" mode=""></image></view>
			<view class="quitBtn" @click="Router.redirectTo({route:{path:'/pages/user/user'}})">退出</view>
			<view class="infor flexColumn">
				<view class="photo">
					<image src="../../static/images/about-img1.png" mode=""></image>
				</view>
				<view class="fs13 mgt10">风飞扬</view>
			</view>
		</view>
		
		<view class="twoBox flex fs13 color3">
			<view class="item flexCenter" @click="Router.navigateTo({route:{path:'/pages/staffUser-resume/staffUser-resume'}})">
				<view>
					<view class="icon"><image src="../../static/images/employeesl-icon.png" mode=""></image></view>
					<view>简历管理</view>
				</view>
			</view>
			<view class="item flexCenter" @click="Router.navigateTo({route:{path:'/pages/staffUser-goOut/staffUser-goOut'}})">
				<view>
					<view class="icon"><image src="../../static/images/employeesl-icon1.png" mode=""></image></view>
					<view>外出登记</view>
				</view>
			</view>
			<view class="item flexCenter" @click="Router.navigateTo({route:{path:'/pages/user-case/user-case'}})">
				<view>
					<view class="icon"><image src="../../static/images/employeesl-icon2.png" mode=""></image></view>
					<view>项目管理</view>
				</view>
			</view>
			<view class="item flexCenter" @click="Router.navigateTo({route:{path:'/pages/staffUser-Extension/staffUser-Extension'}})">
				<view>
					<view class="icon"><image src="../../static/images/employeesl-icon3.png" mode=""></image></view>
					<view>推广客户</view>
				</view>
			</view>
			<view class="item flexCenter" @click="Router.navigateTo({route:{path:'/pages/staffUser-salary/staffUser-salary'}})">
				<view>
					<view class="icon"><image src="../../static/images/employeesl-icon4.png" mode=""></image></view>
					<view>我的薪资</view>
				</view>
			</view>
			<view class="item flexCenter" @click="Router.navigateTo({route:{path:'/pages/staffUser-system/staffUser-system'}})">
				<view>
					<view class="icon"><image src="../../static/images/employeesl-icon5.png" mode=""></image></view>
					<view>公司规定</view>
				</view>
			</view>
			<view class="item flexCenter" @click="Router.navigateTo({route:{path:'/pages/staffUser-leave/staffUser-leave'}})">
				<view>
					<view class="icon"><image src="../../static/images/employeesl-icon6.png" mode=""></image></view>
					<view>请假</view>
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
				showView: false,
				score:'',
				wx_info:{}
			}
		},
		onLoad() {
			const self = this;
			//self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {

		},
	};
</script>

<style>
	
	page{padding-bottom: 60rpx;background-color: #F5F5F5;}
	.headbj{width: 100%;height:400rpx;position: absolute;top: 0;right: 0;bottom: 0;left: 0;}
	.userHead{padding-top: 80rpx;height:400rpx;box-sizing: border-box;}
	.userHead .infor{position:relative ; z-index: 1;}
	.quitBtn{position: absolute;top: 30rpx;right: 30rpx;}
	
	
	.userHead .photo{width: 185rpx;height: 185rpx;padding: 14rpx;box-sizing: border-box;border: 1px solid rgba(255,255,255,0.5);border-radius: 50%;overflow: hidden;}
	.userHead .photo image{width: 100%;height: 100%;border-radius: 50%;box-sizing: border-box;border: 1px solid #fff;}
	
	.twoBox{flex-wrap:wrap ;}
	.twoBox .item{width: 33.33%;height: 250rpx;padding: 30rpx 0;box-sizing: border-box;border-right:1px solid #eee;border-bottom:1px solid #eee;background-color: #fff;}
	.twoBox .item .icon{width: 44rpx;height: 44rpx;display: block;margin: 0 auto 24rpx auto;}
	.twoBox .item .icon image{width: 100%;height: 100%;}
	/* .twoBox .item:nth-last-of-type(2),.twoBox .item:nth-last-of-type(1){border-bottom: 0;} */
</style>
