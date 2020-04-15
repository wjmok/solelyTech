<template>
	<view>
		
		<view class="pdlr4 pdt20 pdb20">
			<view class="fs20 mgb15">会计助理</view>
			<view class="flex fs13"><span class="red">4k-6k</span>/西安/1-3年/学历不限</view>
			<view class="fs12 mgt5 color6">职位诱惑：年底分红13薪</view>
		</view>
		<view class="f5H10"></view>
		
		<view class="pdlr4">
			<view class="fs16 ftw mgb10 pdt20">职位描述</view>
			<view class="flex">
				<view class="jobLable fs13">会计助理</view>
			</view>
			<view class="fs13 mgb5">职位描述</view>
			<view class="xqInfor fs13 color6">
				<view>良好的职业道德，强烈的责任岗，会计初级职称，能处理对账、开票、销售回款、账龄分析等业务，能独立制作销售周报、月报工作。</view>
			</view>
			<view class="fs13 mgb5 mgt10">任职要求</view>
			<view class="xqInfor fs13 color6">
				<view>1、良好的职业道德，强烈的责任感，会计初级职称。</view>
				<view>2、能处理好对账、开票、销售回款、账龄分析等业务，能独立制作销售周报、月报工作。</view>
			</view>
		</view>
		
		<view class="submitbtn" style="padding: 150rpx 0 100rpx 0;">
			<view class="btn"  @click="Router.navigateTo({route:{path:'/pages/sendResumes/sendResumes'}})">投递简历</view>
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
	.jobLable{height: 60rpx;line-height: 58rpx;padding: 0 10px;border-radius: 36rpx;border: 1px solid #EEE;color: #666; margin: 0 20rpx 20rpx 0;}
	.xqInfor view{margin-bottom: 10rpx;}
</style>
