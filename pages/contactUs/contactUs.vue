<template>
	<view>
		<view class="fs13">
			<view class="TopItem flex">
				<view class="flex">
					<image class="icon" src="../../static/images/contact-usl-icon.png" mode=""></image>
				</view>
				<view class="text" @click="call()">联系电话：<span class="pubColor mgl5">15689522562</span></view>
			</view>
			<view class="TopItem flex">
				<view class="flex">
					<image class="icon" src="../../static/images/contact-usl-icon1.png" mode=""></image>
				</view>
				<view class="text">邮箱：<span class="pubColor mgl5">524061853.@qq.com</span></view>
			</view>
			<view class="TopItem flex">
				<view class="flex">
					<image class="icon" src="../../static/images/contact-usl-icon2.png" mode=""></image>
				</view>
				<view class="text">地址：<span class="mgl5">陕西省西安市雁塔区高新大都荟20号楼2007</span></view>
			</view>
		</view>
		<view class="mglr4 flexColumn" style="padding-top: 100rpx;">
			<view class="fs14 mgb10 center">客服二维码</view>
			<view class="ewmPic"><image src="../../static/images/contact-usl-img.png" mode="widthFix"></image></view>
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
			
			call(){
				uni.makePhoneCall({
					phoneNumber:'15689522562'
				});
			},

		},
	};
</script>

<style>
	@import "../../assets/style/editInfor.css";
	@import "../../assets/style/detail.css";
	page{padding-bottom: 60rpx;}
	
	.TopItem{border-bottom: 10rpx solid #F5F5F5;padding: 30rpx 4%;}
	.TopItem .icon{width: 30rpx;height: 30rpx;margin-right: 20rpx;}
	.TopItem .text{width: 90%;}
	
	.ewmPic{width: 230rpx;height: 230rpx;}
</style>
