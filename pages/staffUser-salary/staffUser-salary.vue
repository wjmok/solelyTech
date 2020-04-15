<template>
	<view>
		
		<view class="orderNav flex whiteBj pdtb5 borderB1">
			<view class="tt flexCenter">2019<image class="arrwB" src="../../static/images/to-promotel-icon.png" mode=""></image></view>
			<view class="tt flexCenter">4月<image class="arrwB" src="../../static/images/to-promotel-icon.png" mode=""></image></view>
		</view>
		<view class="editLine">
			<view class="item flex">
				<view class="ll">姓名</view>
				<view class="rr">张萌</view>
			</view>
			<view class="item flex">
				<view class="ll">职位</view>
				<view class="rr">运营</view>
			</view>
			<view class="item flex">
				<view class="ll">底薪</view>
				<view class="rr">1680.00</view>
			</view>
			<view class="item flex">
				<view class="ll">绩效</view>
				<view class="rr">5000.00</view>
			</view>
			<view class="item flex">
				<view class="ll">基本薪资</view>
				<view class="rr">7000.00</view>
			</view>
			<view class="item flex">
				<view class="ll">奖励金额</view>
				<view class="rr">2366.00</view>
			</view>
			<view class="item flex">
				<view class="ll">扣除金额</view>
				<view class="rr flexRowBetween">
					<view>-560.00</view>
					<view class="red">查看详情</view>
				</view>
			</view>
			<view class="item flex">
				<view class="ll">绩效扣除</view>
				<view class="rr">0.00</view>
			</view>
			<view class="item flex">
				<view class="ll">绩效奖励</view>
				<view class="rr">+366.00</view>
			</view>
			<view class="item flex">
				<view class="ll">总计</view>
				<view class="rr red">8366.00</view>
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
				wx_info:{},
				extensionData:3
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
	@import "../../assets/style/orderNav.css";
	@import "../../assets/style/editInfor.css";
	
	page{padding-bottom: 60rpx;background-color: #F5F5F5;}
	
	.editLine .item{padding: 20rpx 2.66%;}
	.editLine .item:last-child{border-bottom: 0;}
	.editLine .item:nth-of-type(2n+1){background-color: #fff;}
	.extension{width: 100%;height: 160rpx;padding: 30rpx;box-sizing: border-box;border-radius: 10rpx;background-color: #fff;margin-top: 30rpx;}
	.extension .photo{width: 100rpx;height: 100rpx;border-radius: 50%;margin-right: 20rpx;}
</style>
