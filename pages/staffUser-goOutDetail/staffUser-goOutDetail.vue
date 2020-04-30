<template>
	<view>
		
		<view class="mglr4 pdtb15">
			<view class="fs15 ftw">起始</view>
			<view class="flex mgt10">
				<view class="mgr25 fs13 color6">时间</view>
				<view>{{mainData.start_time>0?Utils.timeto(mainData.start_time*1000,'ymd-hms'):'-------'}}</view>
			</view>
			<view class="flex mgt10">
				<view class="mgr25 fs13 color6">缘由</view>
				<view>{{mainData.content}}</view>
			</view>
		</view>
		<view class="f5H5"></view>
		<view class="mglr4 pdtb15">
			<view class="fs15 ftw">到达</view>
			<view class="flex mgt10">
				<view class="mgr25 fs13 color6">时间</view>
				<view>{{mainData.arrive_time>0?Utils.timeto(mainData.arrive_time*1000,'ymd-hms'):'-------'}}</view>
			</view>
			<view class="flex picLis">
				<view class="tt" v><image :src="mainData.mainImg&&mainData.mainImg[0]?mainData.mainImg[0].url:''" mode=""></image></view>
			
			</view>
		</view>
		<view class="f5H5"></view>
		<view class="mglr4 pdtb15">
			<view class="fs15 ftw">返程</view>
			<view class="flex mgt10">
				<view class="mgr25 fs13 color6">时间</view>
				<view>{{mainData.back_time>0?Utils.timeto(mainData.back_time*1000,'ymd-hms'):'-------'}}</view>
			</view>
			
		</view>
		<view class="f5H5"></view>
		<view class="mglr4 pdtb15">
			<view class="fs15 ftw">结束</view>
			<view class="flex mgt10">
				<view class="mgr25 fs13 color6">时间</view>
				<view>{{mainData.end_time>0?Utils.timeto(mainData.end_time*1000,'ymd-hms'):'-------'}}</view>
			</view>
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
				caseData:3,
				mainData:{}
			}
		},
		onLoad(options) {
			const self = this;
			self.id = options.id;
			self.$Utils.loadAll(['getMainData'], self);
		},
		
		methods: {
			
			
			getMainData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getStaffToken';
				postData.searchItem = {
					thirdapp_id: 22,
					type:3,
					id:self.id
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData = res.info.data[0];
						//self.mainData.behavior = self.array[self.mainData.behavior];
					}
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.routineGet(postData, callback);
			},
		}
	};
</script>

<style>
	page{padding-bottom: 60rpx;}
	.picLis{flex-wrap: wrap;}
	.picLis .tt{width: 300rpx;height: 200rpx;margin:20rpx 30rpx 0 0;}
	
	
</style>