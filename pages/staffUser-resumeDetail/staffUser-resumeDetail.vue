<template>
	<view>
		
		<view class="myRowBetween pdlr4">
			<view class="item flexRowBetween">
				<view class="ll flex">
					<view class="icon"><image src="../../static/images/resumel-icon.png" mode=""></image></view>
					<view>姓名</view>
				</view>
				<view class="rr">张丹</view>
			</view>
			<view class="item flexRowBetween">
				<view class="ll flex">
					<view class="icon"><image src="../../static/images/resumel-icon1.png" mode=""></image></view>
					<view>电话</view>
				</view>
				<view class="rr">15623561252</view>
			</view>
			<view class="item flexRowBetween">
				<view class="ll flex">
					<view class="icon"><image src="../../static/images/resumel-icon2.png" mode=""></image></view>
					<view>性别</view>
				</view>
				<view class="rr flexEnd">
					<view class="flex"><image class="seltIcon" src="../../static/images/resumel-icon12.png" mode=""></image>女</view>
				</view>
			</view>
			<view class="item flexRowBetween">
				<view class="ll flex">
					<view class="icon"><image src="../../static/images/resumel-icon3.png" mode=""></image></view>
					<view>投递来源</view>
				</view>
				<view class="rr flexEnd" style="flex-wrap: wrap;">
					<view class="flex sourceSelt"><image class="seltIcon" src="../../static/images/resumel-icon12.png" mode=""></image>BPSS直聘</view>
				</view>
			</view>
			<view class="item flexRowBetween">
				<view class="ll flex">
					<view class="icon"><image src="../../static/images/resumel-icon4.png" mode=""></image></view>
					<view>学历</view>
				</view>
				<view class="rr">本科</view>
			</view>
			<view class="item flexRowBetween">
				<view class="ll flex">
					<view class="icon"><image src="../../static/images/resumel-icon5.png" mode=""></image></view>
					<view>毕业院校及专业</view>
				</view>
				<view class="rr">西北大学-会计</view>
			</view>
			<view class="item flexRowBetween">
				<view class="ll flex">
					<view class="icon"><image src="../../static/images/resumel-icon6.png" mode=""></image></view>
					<view>投递职位</view>
				</view>
				<view class="rr">会计</view>
			</view>
			<view class="item flexRowBetween">
				<view class="ll flex">
					<view class="icon"><image src="../../static/images/resumel-icon7.png" mode=""></image></view>
					<view>出生日期</view>
				</view>
				<view class="rr flexEnd">1998年11月12日</view>
			</view>
			<view class="item">
				<view class="flex ll">
					<view class="icon"><image src="../../static/images/resumel-icon8.png" mode=""></image></view>
					<view>工作经历</view>
				</view>
				<view class="pdt10">
					<textarea style="border-color: #d4d4d4;height: 300rpx;" value="火锅是联合国一刚回家客服电话缸发动机kg航天日刚恢复健康的韩国风科技局鹤骨鸡肤肯定会官方都快来收工会发的就是个回复第十三" disabled="disabled" placeholder="请输入" placeholder-class="placeholder" />
				</view>
			</view>
			<view class="item">
				<view class="flex ll">
					<view class="icon"><image src="../../static/images/resumel-icon8.png" mode=""></image></view>
					<view>上传照片</view>
				</view>
				<view class="pdt10 upImg flex">
					<view class="lis"><image src="../../static/images/resumel-img.png" mode=""></image></view>
				</view>
			</view>
		</view>
		<view class="f5H5"></view>
		<view class="myRowBetween pdlr4">
			<view class="item flexRowBetween">
				<view class="ll flex">
					<view class="icon"><image src="../../static/images/resumel-icon10.png" mode=""></image></view>
					<view>处理结果</view>
				</view>
				<view class="rr">
					<picker @change="seltResult" :value="index" :range="array">
						<view class="flexEnd">
							<view class="color9">{{array[index]}}</view>
							<image class="arrowR mgl5" src="../../static/images/0-icon.png" mode=""></image>
						</view>
					</picker>
				</view>
			</view>
			<view class="item">
				<view class="flex ll">
					<view class="icon"><image src="../../static/images/resumel-icon11.png" mode=""></image></view>
					<view>备注</view>
				</view>
				<view class="pdt10">
					<textarea style="border: 0;height: 300rpx;background-color: #F5F5F5;" value="" placeholder="请输入" placeholder-class="placeholder" />
				</view>
			</view>
		</view>
		<view class="f5H5"></view>
		
		<view class="submitbtn" style="padding: 150rpx 0 60rpx 0;">
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
				is_show:false,
				array: ['请选择','处理一','处理二','处理三'],
				index: 0
			}
		},
		onLoad() {
			const self = this;
			// self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
			 seltResult(e) {
				console.log('picker发送选择改变，携带值为', e.target.value)
				this.index = e.target.value
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
	
	.myRowBetween .item:last-child{border-bottom: 0;}
	.myRowBetween .item .ll{width: auto;}
	.myRowBetween .item .rr{width: auto;max-width: 80%;}
	.myRowBetween .ll .icon{width: 28rpx;height: 28rpx;margin-right: 10rpx;}
	.seltIcon{width: 32rpx;height: 32rpx;margin-right: 10rpx;}
	.sourceSelt{margin-left: 50rpx;}
	.sourceSelt:first-child{margin-left: 0;}
	
	.dateInput{width: 75rpx;}
	.myRowBetween .item .dateInput input{text-align: center;line-height: 40rpx;}
	.upLoadBtn{width: 120rpx;height: 120rpx;}
	
	.upImg{flex-wrap: wrap;}
	.upImg .lis{width: 162rpx;height: 162rpx;margin: 0 20rpx 20rpx 0;}
	.upImg .lis:nth-of-type(4n){margin-right: 0;}
</style>
