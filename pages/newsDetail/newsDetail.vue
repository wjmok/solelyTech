<template>
	<view>
		
		<view class="detailBanner">
			<image src="../../static/images/detailsl-img.png" mode=""></image>
		</view>
		
		<view class="mglr4 pdt15 xqInfor" >
			<view class="cont fs13">
				<view>近日：“美团打车”在上海上线“出租车感谢费”，初衷原本是考虑到春节期间供需紧张，为鼓励司机坚持服务，乘客可以自由选择是否给司机感谢费。目前其正在和有关部门就其中涉及的政策法规问题进行沟通，并已经第一时间将该模块下线，就方案进行进一步评估和研究。同时，“美团打车”承诺会与监管部门紧密协作，做好春运服务保障工作。</view>
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
				wx_info:{},
				is_show:false,
				messageData:[{},{},{},{}]
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
	page{padding-bottom:60rpx;}
	
	.detailBanner{width: 100%;height: 400rpx;box-sizing: border-box;overflow: hidden;}
	
	.xqInfor .cont{line-height: 44rpx;}
	.xqInfor .cont view{padding-bottom: 10rpx;}
	
	
</style>
