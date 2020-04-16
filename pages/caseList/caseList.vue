<template>
	<view>
		
		<view class="pdlr4">
			<view class="flex menuTit pdtb20 fs13" @click="categoryShow()">
				<image src="../../static/images/casel-icon.png" style="width: 36rpx;height: 30rpx;margin-right: 10rpx;" mode=""></image>小程序
			</view>
			
			<view class="black-bj" style="top: 0rpx;" v-show="is_show"></view>
			<view class="categoryBox" v-show="is_categoryShow">
				<view class="pdt20 fs14 ftw">类型</view>
				<view class="typeNav flex fs13 pdt10 borderB1">
					<view class="tt" :class="typeCurr==index?'on':''" @click="typeChange(index)" v-for="(item,index) in typeData" :key="index">{{item}}</view>
				</view>
				<view class="pdt20 fs14 ftw">行业</view>
				<view class="industryNav flex fs13 pdt5 color6">
					<view class="tt" :class="industryCurr==index?'on':''" @click="industryChange(index)" v-for="(item,index) in industryData" :key="index">{{item}}</view>
				</view>
				
				<view class="pdtb25 flexCenter">
					<view style="width: 36rpx;height: 36rpx;" @click="categoryShow()"><image src="../../static/images/casel-icon1.png" mode=""></image></view>
				</view>
			</view>
			
			<view class="flexRowBetween caseList">
				<view class="item radius10 pr boxShaow" v-for="(item,index) in caseData" :key="index" @click="Router.navigateTo({route:{path:'/pages/caseDetail/caseDetail'}})">
					<view class="pic"><image src="../../static/images/casel-img1.png" mode=""></image></view>
					<view class="tit fs13">酒便利APP</view>
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
					<image src="../../static/images/nabar2-a.png" />
				</view>
				<view class="text this-text">行业案例</view>
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
				is_show:false,
				is_categoryShow:false,
				typeCurr:0,
				typeData:['小程序','APP','公众号','网站','粮油','生鲜','蛋类'],
				industryCurr:0,
				industryData:['餐饮','履行','商场','服装','旅游','母婴','社交','餐饮','履行','商场','服装','旅游','母婴','社交'],
				caseData:[{},{},{},{}],
				
			}
		},
		onLoad() {
			const self = this;
			// self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
			categoryShow(){
				const self = this;
				self.is_show = !self.is_show;
				self.is_categoryShow = !self.is_categoryShow;
				
			},
			typeChange(index){
				const self = this;
				self.typeCurr = index
			},
			industryChange(index){
				const self = this;
				self.industryCurr = index
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
	@import "../../assets/style/navbar.css";
	
	page{padding-bottom: 140rpx;}
	
	.caseList{flex-wrap: wrap;align-items: flex-start;}
	.caseList .item{width: 345rpx;height: 692rpx;margin-bottom: 30rpx;background: #fff;overflow: hidden;}
	.caseList .item .pic{width: 100%;height: 612rpx;}
	.caseList .item .tit{padding: 20rpx 4%;text-align: center;}
	
	.categoryBox{position: fixed;top: 0rpx;left: 0;right: 0;background-color: #fff;padding: 0 2.6%;box-sizing: border-box; z-index: 45;border-top: 1px solid #eee;}
	
	/* 类型 */
	.typeNav{flex-wrap: wrap;}
	.typeNav .tt{width: 150rpx;box-sizing: border-box;text-align: center;line-height: 50rpx;height: 54rpx;border-radius: 24rpx 0 24rpx 0;border: 1px solid #eee;margin: 0 36rpx 30rpx 0;}
	.typeNav .tt:nth-of-type(4n){margin-right: 0;}
	.typeNav .tt.on{background-color: #21c3d4;color: #fff;border: 0;}
	
	/* 行业 */
	.industryNav{flex-wrap: wrap;}
	.industryNav .tt{width: 150rpx;box-sizing: border-box;text-align: center;border-bottom: 1px solid #eee;margin: 0 36rpx 30rpx 0;padding: 16rpx 0;}
	.industryNav .tt:nth-of-type(4n){margin-right: 0;}
	.industryNav .tt.on{color: #21c3d4;border-bottom: 1px solid #21c3d4;}
</style>
