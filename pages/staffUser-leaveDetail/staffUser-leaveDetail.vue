<template>
	<view>
		
		<view class="editLine pdlr4">
			<view class="item flexRowBetween">
				<view class="ll">请假事由</view>
				<view class="rr">
					<textarea class="f5bj" v-model="mainData.content" placeholder="" disabled placeholder-class="placeholder" />
				</view>
			</view>
			<view class="item flexRowBetween">
				<view class="ll">请假类型</view>
				<view class="rr flex">
					<!-- <picker @change="seltResult" :value="index" :range="array"> -->
						<view class="seltStyle flexRowBetween">
							<view class="">{{mainData.behavior}}</view>
							<!-- <view style="width: 20rpx;height: 14rpx;"><image src="../../static/images/leave-icon.png" mode=""></image></view> -->
						</view>
					<!-- </picker> -->
				</view>
			</view>
			<view class="item flexRowBetween">
				<view class="ll">起止时间</view>
				<view class="rr">
					<view class="seltTime">
						<view class="input">{{Utils.timeto(mainData.start_time,'ymd-hms')}}</view>
					</view>
					<view class="seltTime mgt15">
						<view class="input">{{Utils.timeto(mainData.end_time,'ymd-hms')}}</view>
					</view>
				</view>
			</view>
		</view>
		
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				Utils:this.$Utils,
				array: ['事假','病假','年假','其他'],
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
					type:4,
					id:self.id
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData = res.info.data[0];
						self.mainData.behavior = self.array[self.mainData.behavior];
					}
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.routineGet(postData, callback);
			},
		}
	};
</script>

<style>
	@import "../../assets/style/editInfor.css";
	page{padding-bottom: 60rpx;}
	
	.editLine .item{border-bottom: 0;padding: 30rpx 0;}
	.editLine .item .rr{color: #666;font-size: 26rpx;}
	.editLine .item textarea{height: 260rpx;box-sizing: border-box;}
	.seltStyle{width: 340rpx;height: 60rpx;border: 1px solid #eee;padding: 0 20rpx;box-sizing: border-box;}
	
	.seltTime{width: 340rpx;height: 60rpx;border: 1px solid #eee;padding: 0 20rpx;box-sizing: border-box;margin-bottom: 30rpx;}
</style>
