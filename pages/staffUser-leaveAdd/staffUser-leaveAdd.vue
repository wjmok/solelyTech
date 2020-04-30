<template>
	<view>

		<view class="editLine pdlr4">
			<view class="item flexRowBetween">
				<view class="ll"><span class="red mgr5">*</span>请假事由</view>
				<view class="rr">
					<textarea class="f5bj" v-model="submitData.content" placeholder="请填写" placeholder-class="placeholder" />
					</view>
			</view>
			<view class="item flexRowBetween">
				<view class="ll"><span class="red mgr5">*</span>请假类型</view>
				<view class="rr flex">
					<picker @change="seltResult" :value="index" :range="array">
						<view class="seltStyle flexRowBetween">
							<view class="">{{array[index]}}</view>
							<view style="width: 20rpx;height: 14rpx;"><image src="../../static/images/leave-icon.png" mode=""></image></view>
						</view>
					</picker>
					<!-- <input type="text" maxlength="11" value="" placeholder="请输入" placeholder-class="placeholder" /> -->
				</view>
			</view>
			<view class="item flexRowBetween">
				<view class="ll"><span class="red mgr5">*</span>起止时间</view>
				<view class="rr flexRowBetween" style="flex-wrap: wrap;">
					<view class="seltTime">
						<view class="flexRowBetween">
							<view>
								<picker mode="date"  @change="changeStartDate">
									<view>{{startDate!=''?startDate:'请选择'}}</view>
								</picker>
							</view>
							<view class="arrowB"><image src="../../static/images/leave-icon.png" mode=""></image></view>
						</view>
					</view>
					<view class="seltTime">
						<view class="flexRowBetween">
							<view>
								<picker mode="time"  @change="changeStartTime">
									<view>{{startTime!=''?startTime:'请选择'}}</view>
								</picker>
							</view>
							<view class="arrowB"><image src="../../static/images/leave-icon.png" mode=""></image></view>
						</view>
					</view>
					<view class="seltTime">
						<view class="flexRowBetween">
							<view>
								<picker mode="date"  @change="changeEndDate">
									<view>{{endDate!=''?endDate:'请选择'}}</view>
								</picker>
							</view>
							<view class="arrowB"><image src="../../static/images/leave-icon.png" mode=""></image></view>
						</view>
					</view>
					<view class="seltTime">
						<view class="flexRowBetween">
							<view>
								<picker mode="time"  @change="changeEndTime">
									<view>{{endTime!=''?endTime:'请选择'}}</view>
								</picker>
							</view>
							<view class="arrowB"><image src="../../static/images/leave-icon.png" mode=""></image></view>
						</view>
					</view>
				</view>
			</view>
		</view>
		
		<view class="submitbtn" style="padding-top: 200rpx;">
			<view class="btn" @click="Utils.stopMultiClick(submit)">提交</view>
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
				index: 0,
				submitData:{
					type:4,
					content:'',
					start_time:'',
					end_time:''
				},
				startDate:'',
				startTime:'',
				endDate:'',
				endTime:''
			}
		},
		
		onLoad() {
			const self = this;
			// self.$Utils.loadAll(['getMainData'], self);
		},
		
		methods: {
			
			
			changeStartDate(e){
			    const self = this;
			    self.startDate = e.detail.value;
			},
			
			changeStartTime(e) {
			    const self = this;
			    if(self.startDate){
					self.startTime = e.detail.value;
			        self.submitData.start_time = self.$Utils.timeToTimestamp(self.startDate+' '+e.detail.value)*1000;
				}else{
					self.$Utils.showToast('请选择起始日期','none',1000)
				};
			},
			
			changeEndDate(e){
			    const self = this;
				console.log(e)
			    self.endDate = e.detail.value;
			},
			
			changeEndTime(e) {
			    const self = this;
			    if(self.endDate){
					self.endTime = e.detail.value;
			        self.submitData.end_time = self.$Utils.timeToTimestamp(self.endDate+' '+e.detail.value)*1000;
				}else{
					self.$Utils.showToast('请选择起始日期','none',1000)
				};
			},
			
			seltResult(e) {
				console.log('picker发送选择改变，携带值为', e.target.value)
				this.index = e.target.value
			},
			
			routineAdd() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getStaffToken';
				postData.searchItem = {
					user_no:uni.getStorageSync('user_info').user_no
				};
				postData.data = {};
				postData.data = self.$Utils.cloneForm(self.submitData);
				postData.data.behavior = self.index;
				const callback = (data) => {				
					if (data.solely_code == 100000) {					
						self.$Utils.showToast('申请成功', 'none', 1000)
						setTimeout(function() {
							uni.navigateBack({
								delta:1
							})
						}, 1000);
					} else {
						uni.setStorageSync('canClick', true);
						self.$Utils.showToast(data.msg, 'none', 1000)
					}	
				};
				self.$apis.routineAdd(postData, callback);
			},
			
			submit() {
				const self = this;
				uni.setStorageSync('canClick', false);
				const pass = self.$Utils.checkComplete(self.submitData);
				console.log('pass', pass);
				console.log('self.submitData',self.submitData)
				if (pass) {	
					self.routineAdd();
				} else {
					uni.setStorageSync('canClick', true);
					self.$Utils.showToast('请输入留言内容', 'none')
				};
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
	
	.seltTime{width: 48%;height: 60rpx;border: 1px solid #eee;padding: 0 20rpx;box-sizing: border-box;margin-bottom: 30rpx;}
	.seltTime>view{width: 100%;height: 100%;}
	.arrowB{width: 20rpx;height: 14rpx;}
</style>
