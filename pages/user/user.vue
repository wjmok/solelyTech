<template>
	<view>
		<view class="userHead pr">
			<view class="headbj"><image src="../../static/images/about-img.png" mode=""></image></view>
			<view class="infor flexColumn">
				<view class="photo">
					<image src="../../static/images/about-img1.png" mode=""></image>
				</view>
				<view class="fs13 mgt10">风飞扬</view>
			</view>
		</view>
		
		<view class="twoBox flex fs13 color3">
			<view class="item flexCenter" @click="Router.navigateTo({route:{path:'/pages/userInfor/userInfor'}})">
				<view>
					<view class="icon"><image src="../../static/images/about-icon.png" mode=""></image></view>
					<view>我的信息</view>
				</view>
				
			</view>
			<view class="item flexCenter" @click="Router.navigateTo({route:{path:'/pages/user-case/user-case'}})">
				<view>
					<view class="icon"><image src="../../static/images/about-icon1.png" mode=""></image></view>
					<view>项目管理</view>
				</view>
			</view>
			<view class="item flexCenter" @click="Router.navigateTo({route:{path:'/pages/user-myMessages/user-myMessages'}})">
				<view>
					<view class="icon"><image src="../../static/images/about-icon2.png" mode=""></image></view>
					<view>我的留言</view>
				</view>
			</view>
			<view class="item flexCenter" @click="Router.navigateTo({route:{path:'/pages/staffLogin/staffLogin'}})">
				<view>
					<view class="icon"><image src="../../static/images/about-icon3.png" mode=""></image></view>
					<view>员工登录</view>
				</view>
			</view>
			<view class="item flexCenter" @click="Router.navigateTo({route:{path:'/pages/sendResumes/sendResumes'}})">
				<view>
					<view class="icon"><image src="../../static/images/about-icon4.png" mode=""></image></view>
					<view>投递简历</view>
				</view>
			</view>
		</view>
		
		
		<!--底部tab键-->
		<view class="navbar">
			<view class="navbar_item" @click="Router.redirectTo({route:{path:'/pages/index/index'}})">
				<view class="nav_img">
					<image src="../../static/images/nabar1.png" />
				</view>
				<view class="text">首页</view>
			</view>
			<view class="navbar_item" @click="Router.redirectTo({route:{path:'/pages/caseList/caseList'}})">
				<view class="nav_img">
					<image src="../../static/images/nabar2.png" />
				</view>
				<view class="text">行业案例</view>
			</view>
			<view class="navbar_item" @click="Router.redirectTo({route:{path:'/pages/newsCenter/newsCenter'}})" >
				<view class="nav_img">
					<image src="../../static/images/nabar3.png" />
				</view>
				<view class="text">资讯中心</view>
			</view>
			<view class="navbar_item" @click="Router.redirectTo({route:{path:'/pages/user/user'}})" >
				<view class="nav_img">
					<image src="../../static/images/nabar4-a.png" />
				</view>
				<view class="text this-text">个人中心</view>
			</view>
		</view>
		<!--底部tab键 end-->
		
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
	@import "../../assets/style/editInfor.css";
	@import "../../assets/style/navbar.css";
	page{padding-bottom: 180rpx;background-color: #F5F5F5;}
	.headbj{width: 100%;height:400rpx;position: absolute;top: 0;right: 0;bottom: 0;left: 0;}
	.userHead{padding-top: 80rpx;height:400rpx;box-sizing: border-box;}
	.userHead .infor{position:relative ; z-index: 1;}
	
	.userHead .photo{width: 185rpx;height: 185rpx;padding: 14rpx;box-sizing: border-box;border: 1px solid rgba(255,255,255,0.5);border-radius: 50%;overflow: hidden;}
	.userHead .photo image{width: 100%;height: 100%;border-radius: 50%;box-sizing: border-box;border: 1px solid #fff;}
	
	.twoBox{flex-wrap:wrap ;}
	.twoBox .item{width: 33.33%;height: 250rpx;padding: 30rpx 0;box-sizing: border-box;border-right:1px solid #eee;border-bottom:1px solid #eee;background-color: #fff;}
	.twoBox .item .icon{width: 44rpx;height: 44rpx;display: block;margin: 0 auto 24rpx auto;}
	.twoBox .item .icon image{width: 100%;height: 100%;}
	/* .twoBox .item:nth-last-of-type(2),.twoBox .item:nth-last-of-type(1){border-bottom: 0;} */
</style>
