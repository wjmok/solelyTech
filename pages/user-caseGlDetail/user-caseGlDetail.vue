<template>
	<view>
		
		<view class="editLine">
			<view class="item flex">
				<view class="ll flex"><image class="icon" src="../../static/images/projectl-icon0.png" mode=""></image>签订时间：</view>
				<view class="rr">2019.04.15</view>
			</view>
			<view class="item flex">
				<view class="ll flex"><image class="icon" src="../../static/images/projectl-icon1.png" mode=""></image>合同编号：</view>
				<view class="rr">1645455212</view>
			</view>
			<view class="item flex">
				<view class="ll flex"><image class="icon" src="../../static/images/projectl-icon2.png" mode=""></image>项目名称：</view>
				<view class="rr">百舌鸟小程序</view>
			</view>
			<view class="item flex">
				<view class="ll flex"><image class="icon" src="../../static/images/projectl-icon3.png" mode=""></image>客户名称：</view>
				<view class="rr">张丹</view>
			</view>
			<view class="item flex">
				<view class="ll flex"><image class="icon" src="../../static/images/projectl-icon4.png" mode=""></image>手机号码：</view>
				<view class="rr">18023526256</view>
			</view>
			<view class="item flex">
				<view class="ll flex"><image class="icon" src="../../static/images/projectl-icon5.png" mode=""></image>合同金额：</view>
				<view class="rr">230000</view>
			</view>
			<view class="item flex">
				<view class="ll flex"><image class="icon" src="../../static/images/projectl-icon6.png" mode=""></image>支付金额：</view>
				<view class="rr">10000</view>
			</view>
			<view class="item flex">
				<view class="ll flex"><image class="icon" src="../../static/images/projectl-icon7.png" mode=""></image>项目状态：</view>
				<view class="rr">开发中</view>
			</view>
			<view class="item">
				<view>
					<view class="ll flex"><image class="icon" src="../../static/images/projectl-icon8.png" mode=""></image>项目图片：</view>
				</view>
				<view class="mgt10">
					<scroll-view class="imgList" scroll-x>
						<view class="tt" v-for="(item,index) in imgListData" :key="index"  @click="imglisShow"><image :src="item" mode=""></image></view>
					</scroll-view>
				</view>
			</view>
			<view class="item">
				<view>
					<view class="ll flex"><image class="icon" src="../../static/images/projectl-icon9.png" mode=""></image>项目文档：</view>
				</view>
				<view class="">
					<view class="textFile flexRowBetween" v-for="(item,index) in textFileData" :key="index">
						<view class="Ltit flex">
							<view class="dian mgr10"></view>
							<view class="text avoidOverflow">项目款到发货打包就看见了换个卡讽德诵功</view>
						</view>
						<view class="Rbtn flexEnd">
							<image class="loadIcon" src="../../static/images/projectl-icon10.png" mode=""></image>
							<view>下载</view>
						</view>
					</view>
				</view>
			</view>
		</view>
		
		<!-- 图片弹框 -->
		<view class="black-bj" v-show="is_show"></view>
		
		<view class="banner-box pdlr4" v-show="is_imglisShow">
			<view class="banner">
				<swiper class="swiper-box" indicator-dots="true" autoplay="true" interval="3000" duration="1000" indicator-active-color="#39c9d8">
					<block v-for="(item,index) in imgListData" :key="index">
						<swiper-item class="swiper-item">
							<image :src="item" class="slide-image" />
						</swiper-item>
					</block>
				</swiper>
			</view>
			<view class="closeBtn" @click="imglisShow">×</view>
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
				imgListData:[
					'../../static/images/projectl-img.png',
					'../../static/images/projectl-img.png',
					'../../static/images/projectl-img.png',
					'../../static/images/projectl-img.png'
				],
				textFileData:3,
				is_imglisShow:false
			}
		},
		onLoad() {
			const self = this;
			// self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
			imglisShow(){
				const self = this;
				self.is_show = !self.is_show;
				self.is_imglisShow = !self.is_imglisShow;
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
	
	.editLine .item:last-child{border-bottom: 0;}
	.editLine .item .ll{color: #666;font-size: 26rpx;}
	.editLine .item .ll .icon{width:28rpx;height:28rpx;margin-right: 10rpx;}
	.imgList{white-space: nowrap;}
	.imgList .tt{display: inline-block;width: 210rpx;height: 140rpx;margin-right:20rpx; overflow: hidden;}
	
	.textFile{margin-top: 20rpx;}
	.textFile .Ltit{width: 75%;}
	.textFile .Ltit .dian{width: 10rpx;height: 10rpx;border-radius: 50%;background-color: #222;}
	.textFile .Ltit .text{width: 90%;}
	.loadIcon{width: 32rpx;height: 32rpx;margin-right: 10rpx;}
	
	.banner-box{width: 100%;position: fixed;top: 50%;left: 50%;transform: translate(-50%,-50%); z-index: 45;box-sizing: border-box;}
	.swiper-box {height: 480rpx;box-sizing: border-box;overflow: hidden;background-color: #fff;padding: 30rpx;}
	.swiper-box swiper-item{width: 100%;height: 420rpx;box-sizing: border-box;overflow: hidden;}
	.swiper-box swiper-item image{width: 100%;height: 100%;box-sizing: border-box;}
</style>
