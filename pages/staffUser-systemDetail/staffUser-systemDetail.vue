<template>
	<view>
		
		<view class="xqInfor fs13  pdlr4 whiteBj">
			<view>1、公司规章制度是公司用于规范公司全体成员及公司所有经济活动的标准和规定，它是公司内部经济责任制的具体化</view>
			<view>2、公司规章制度大致可分为公司基本制度、公司工作制度和公司责任制度。公司规章制度的制定，应体现公司经济活动的特点和要求。</view>
			<view>3、公司规章制度的制定要以《劳动法》为具体依据，不能出现违背相关法律条款。</view>
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
	
	.xqInfor{padding: 30rpx 2.666%;}
	.xqInfor view{margin-bottom: 20rpx;line-height: 44rpx;}
</style>
