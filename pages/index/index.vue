<template>
	<view>
		
		<view class="homeHead">
			<view class="banner-box">
				<image src="../../static/images/home-banenr.png" mode=""></image>
			</view>
		</view>
		
		<view class="flexRowBetween homeNav">
			<view class="half flexCenter">
				<view class="item flexColumn" @click="Router.navigateTo({route:{path:'/pages/hotjob/hotjob'}})">
					<view class="icon"><image src="../../static/images/home-icon.png" mode=""></image></view>
					<view class="tit mgt10" style="color: #9087f9;">热招职位</view>
					<view class="text">期待加入</view>
				</view>
			</view>
			<view class="half rr">
				<view class="item flex">
					<view class="icon"><image src="../../static/images/home-icon1.png" mode=""></image></view>
					<view>
						<view class="tit"  style="color: #5cdfdd;">一键导航</view>
						<view class="text">期待到来</view>
					</view>
				</view>
				<view class="item flex" @click="Router.navigateTo({route:{path:'/pages/contactUs/contactUs'}})">
					<view class="icon"><image src="../../static/images/home-icon2.png" mode=""></image></view>
					<view>
						<view class="tit" style="color: #ff79fd;">联系我们</view>
						<view class="text">为您服务</view>
					</view>
				</view>
			</view>
		</view>
		<view class="f5H5"></view>
		
		<view class="pdlr4">
			<view class="Big-title fs15 pdt20 ftw">西安纯粹云信息科技有限公司</view>
			<view class="flex pdt5" style="flex-wrap: wrap;">
				<view class="starBox mgr5">
					<image src="../../static/images/home-icon3.png" mode=""></image>
					<image src="../../static/images/home-icon3.png" mode=""></image>
					<image src="../../static/images/home-icon3.png" mode=""></image>
					<image src="../../static/images/home-icon3.png" mode=""></image>
					<image src="../../static/images/home-icon3.png" mode=""></image>
				</view>
				<view class="fs11">小程序、公众号、网站、APP开发、LOGO设计</view>
			</view>
			<view class="flexRowBetween pdt30 pdb25 dataList center">
				<view class="item">
					<view class="fs20 ftw">2016</view>
					<view class="mgt10 fs12 color6">开始于</view>
				</view>
				<view class="item">
					<view class="fs20 ftw">860+</view>
					<view class="mgt10 fs12 color6">服务于</view>
				</view>
				<view class="item">
					<view class="fs20 ftw">560+</view>
					<view class="mgt10 fs12 color6">在线项目</view>
				</view>
			</view>
			
			<view class="fs13" style="line-height: 50rpx;">纯粹科技创世至今，以雄厚的技术团队和专业的设计团队，帮助中小企业快速搭建移动互联网平台，公司自立于互联网的大环境下，致力于拓新型营销模式，用心打造值得信赖的多元化移动互联网机构。成为中小型企业在移动互联网领域最为信任的合作伙伴，可提供多个行业的解决方案，助力企业实现品牌树立，形象塑造，营销推广等。</view>
			<view class="w pdt20"><image src="../../static/images/home-img2.png" mode="widthFix"></image></view>
		</view>
		
		
		<!--底部tab键-->
		<view class="navbar">
			<view class="navbar_item" @click="Router.redirectTo({route:{path:'/pages/index/index'}})">
				<view class="nav_img">
					<image src="../../static/images/nabar1-a.png" />
				</view>
				<view class="text this-text">首页</view>
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
					<image src="../../static/images/nabar4.png" />
				</view>
				<view class="text">个人中心</view>
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
	@import "../../assets/style/navbar.css";
	@import "../../assets/style/star.css";
	
	page{padding-bottom: 140rpx;}	
	
	.banner-box{width: 100%;height: 360rpx;}
	
	.homeNav .half{width: 50%;height: 300rpx;box-sizing: border-box;}
	.homeNav .half:first-child{border-right: 1px solid #eee;}
	.homeNav .half .item{ box-sizing: border-box;padding: 30rpx;}
	.homeNav .half .item .icon{width: 90rpx;height: 90rpx;border-radius: 50%;}
	.homeNav .half.rr .item{width: 100%;height: 150rpx; box-sizing: border-box;}
	.homeNav .half.rr .item:first-child{border-bottom: 1px solid #eee;}
	.homeNav .half.rr .icon{margin-right: 20rpx;}
	.homeNav .half .tit{font-weight: bold;font-size: 30rpx;}
	.homeNav .half .text{font-size: 24rpx;color: #666;}
	
	.dataList .item{width: 33.33%;}
</style>
