<template>
	<view>
		
		<view class=" mglr4 pdtb15">
			<textarea v-model="submitData.content" placeholder="请输入缘由" placeholder-class="placeholder" />
		</view>
		<view class="f5H10"></view>
		
		<view class="submitbtn" style="padding: 150rpx 0 60rpx 0;">
			<view class="btn"  @click="Utils.stopMultiClick(submit)">提交</view>
		</view>
		
	</view>
</template>

<script>
	export default {
		
		data() {
			return {
				Router:this.$Router,
				Utils:this.$Utils,
				submitData:{
					type:3,
					content:'',
					latitude:'',
					longitude:''
				},
			}
		},
		
		onLoad() {
			const self = this;
			self.$Utils.loadAll(['getLocation'], self);
		},
		
		methods: {
			
			getLocation(){
				const self = this;
				uni.getLocation({
				    type: 'wgs84',
				    success: function (res) {
						self.submitData.latitude = res.latitude;
						self.submitData.longitude = res.longitude;
				    }
				});
				self.$Utils.finishFunc('getLocation');
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
				postData.data.start_time = Date.parse(new Date())/1000;
				const callback = (data) => {				
					if (data.solely_code == 100000) {					
						self.$Utils.showToast('添加成功', 'none', 1000)
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
					self.$Utils.showToast('请输入外出原因', 'none')
				};
			},
		}
	};
</script>

<style>
	@import "../../assets/style/editInfor.css";
	page{padding-bottom: 60rpx;}
	
	textarea{border: 0;height: 400rpx;}
	
</style>
