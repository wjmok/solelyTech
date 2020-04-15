<template>
	<view>
		
		<view class="pdlr4">
			<view class="newsList fs14 flexRowBetween pdt15">
				<view class="item" v-for="(item,index) in newsData" :key="index" @click="Router.navigateTo({route:{path:'/pages/newsDetail/newsDetail'}})">
					<view class="pic"><image src="../../static/images/informationl-img.png" mode=""></image></view>
					<view class="tit">APP开发须知</view>
				</view>
			</view>
			
			<!-- 无数据 -->
			<view class="nodata"><image src="../../static/images/nodata.png" mode=""></image></view>
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
			<view class="navbar_item" @click="Router.redirectTo({route:{path:'/pages/caseList/caseList'}})" >
				<view class="nav_img">
					<image src="../../static/images/nabar3-a.png" />
				</view>
				<view class="text this-text">资讯中心</view>
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
				is_show:false,
				newsData:[{},{},{},{},{},{},{},{}],
				
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
	
	page{padding-bottom: 140rpx;}
	
	.newsList{flex-wrap: wrap;align-items: flex-start;}
	.newsList .item{width: 340rpx;height: 280rpx;margin-bottom:30rpx;background: #fff;overflow: hidden;}
	.newsList .item .pic{width: 100%;height: 220rpx;}
	.newsList .item .tit{padding: 20rpx 4% 0 4%;text-align: center;}
	
	
</style>
