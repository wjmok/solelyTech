<template>
	<view>
		
		<view class="editLine">
			<view class="item flex">
				<view class="ll flex"><image class="icon" src="../../static/images/projectl-icon0.png" mode=""></image>签订时间：</view>
				<view class="rr">{{Utils.timeto(mainData.sign_time,'ymd')}}</view>
			</view>
			<view class="item flex">
				<view class="ll flex"><image class="icon" src="../../static/images/projectl-icon1.png" mode=""></image>合同编号：</view>
				<view class="rr">缺少字段</view>
			</view>
			<view class="item flex">
				<view class="ll flex"><image class="icon" src="../../static/images/projectl-icon2.png" mode=""></image>项目名称：</view>
				<view class="rr">{{mainData.name}}</view>
			</view>
			<view class="item flex">
				<view class="ll flex"><image class="icon" src="../../static/images/projectl-icon3.png" mode=""></image>客户名称：</view>
				<view class="rr">{{mainData.client}}</view>
			</view>
			<view class="item flex">
				<view class="ll flex"><image class="icon" src="../../static/images/projectl-icon4.png" mode=""></image>手机号码：</view>
				<view class="rr">{{mainData.phone}}</view>
			</view>
			<view class="item flex">
				<view class="ll flex"><image class="icon" src="../../static/images/projectl-icon5.png" mode=""></image>合同金额：</view>
				<view class="rr">{{mainData.total_amount}}</view>
			</view>
			<view class="item flex">
				<view class="ll flex"><image class="icon" src="../../static/images/projectl-icon6.png" mode=""></image>支付金额：</view>
				<view class="rr">{{mainData.payment.payment}}</view>
			</view>
			<view class="item flex">
				<view class="ll flex"><image class="icon" src="../../static/images/projectl-icon7.png" mode=""></image>项目状态：</view>
				<view class="rr" v-if="mainData.sign_status==0">立项中</view>
				<view class="rr" v-if="mainData.sign_status==1">开发中</view>
				<view class="rr" v-if="mainData.sign_status==2">交付测试</view>
				<view class="rr" v-if="mainData.sign_status==3">已交接</view>
				<view class="rr" v-if="mainData.sign_status==4">已完结</view>
				<view class="rr" v-if="mainData.sign_status==5">烂尾</view>
			</view>
			<view class="item">
				<view>
					<view class="ll flex"><image class="icon" src="../../static/images/projectl-icon8.png" mode=""></image>项目图片：</view>
				</view>
				<view class="mgt10">
					<scroll-view class="imgList" scroll-x>
						<view class="tt" v-for="(item,index) in mainData.mainImg" :key="index"  
						@click="imglisShow"><image :src="item.url" mode=""></image></view>
					</scroll-view>
				</view>
			</view>
			<view class="item">
				<view>
					<view class="ll flex"><image class="icon" src="../../static/images/projectl-icon9.png" mode=""></image>项目文档：</view>
				</view>
				<view class="">
					<view class="textFile flexRowBetween" v-for="(item,index) in mainData.file" :key="index">
						<view class="Ltit flex">
							<view class="dian mgr10"></view>
							<view class="text avoidOverflow">{{item.title}}</view>
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
				<swiper class="swiper-box" indicator-dots="true"  interval="3000" duration="1000" indicator-active-color="#39c9d8">
					<block v-for="(item,index) in mainData.mainImg" :key="index">
						<swiper-item class="swiper-item">
							<image :src="item.url" class="slide-image" />
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
				Utils:this.$Utils,
				is_show: false,
				is_imglisShow:false,
				mainData:{}
			}
		},
		
		onLoad(options) {
			const self = this;
			self.id = options.id;
			self.$Utils.loadAll(['getMainData'], self);
		},
		
		methods: {
			
			imglisShow(){
				const self = this;
				self.is_show = !self.is_show;
				self.is_imglisShow = !self.is_imglisShow;
			},
			
			getMainData(){
			    var self = this;
			    var postData = {};
				postData.tokenFuncName = 'getProjectToken';
			    postData.searchItem = {
					id:self.id,
					thirdapp_id:22,
				};
				postData.getAfter = {
					payment:{
						tableName:'Payment',
						middleKey:'project_no',
						key:'project_no',
						condition:'=',
						searchItem:{
							status:1
						},
						compute:{
							payment:['sum','money',{status:1}]
						}
					}
				};
			    var callback = function(res){
			        if(res.info.data.length>0&&res.info.data[0]){
						self.mainData  =res.info.data[0];
						const regex = new RegExp('<img', 'gi');
						self.mainData.content = self.mainData.content.replace(regex, `<img style="max-width: 100%;"`);
			        };    
					self.$Utils.finishFunc('getMainData');
			    };
				self.$apis.projectGet(postData, callback);
			},
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
