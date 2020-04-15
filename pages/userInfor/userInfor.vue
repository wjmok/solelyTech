<template>
	<view>
		
		<view class="myRowBetween pdlr4">
			<view class="item flexRowBetween">
				<view class="ll">您的姓名</view>
				<view class="rr">
					<input type="text" value="" placeholder="请输入" placeholder-class="placeholder" />
				</view>
			</view>
			<view class="item flexRowBetween">
				<view class="ll">联系电话</view>
				<view class="rr">
					<input type="text" maxlength="11" value="" placeholder="请输入" placeholder-class="placeholder" />
				</view>
			</view>
			<view class="item flexRowBetween">
				<view class="ll">验证码</view>
				<view class="rr flexEnd">
					<view style="width: 50%;"><input type="text" value="" placeholder="请输入" placeholder-class="placeholder" /></view>
					<view class="pubColor mgl15">获取验证码</view>
				</view>
			</view>
			<view class="item flexRowBetween">
				<view class="ll">地址</view>
				<view class="rr">
					<input type="text" maxlength="11" value="" placeholder="请输入" placeholder-class="placeholder" />
				</view>
			</view>
			<view class="item flexRowBetween">
				<view class="ll">公司名称</view>
				<view class="rr">
					<input type="text" maxlength="11" value="" placeholder="请输入" placeholder-class="placeholder" />
				</view>
			</view>
		</view>
		
		<view class="submitbtn" style="padding-top: 200rpx;">
			<view class="btn">提交</view>
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
	@import "../../assets/style/editInfor.css";
	page{padding-bottom: 60rpx;}
	
	.myRowBetween .item .ll{width: auto;}
	.myRowBetween .item .rr{width: 75%;}
	
</style>
