<template>
	<view>
		
		<view class="">
			
			<view class="mapBox">
				<map style="width: 100%; height: 400px;" :latitude="latitude" :longitude="longitude" :markers="covers">
				</map>
			</view>
			
			<view class="camera flexCenter">
				<view class="flexColumn">
					<view class="btn mgb10" @click="upLoadImg('mainImg')" v-if="submitData.mainImg.length==0"><image src="../../static/images/to-go-outl-icon1.png" mode=""></image></view>
					
					<view class="btn mgb10"  v-if="submitData.mainImg.length>0"><image :src="submitData.mainImg&&submitData.mainImg[0]?submitData.mainImg[0].url:''" mode=""></image></view>
					<view>拍照</view>
				</view>
			</view>
			
			<view class="submitbtn">
				<button class="btn"  @click="Utils.stopMultiClick(submit)">确定</button>
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
				id:0, // 使用 marker点击事件 需要填写id
				title: 'map',
				latitude: '',
				longitude: '',
				covers: [{
					latitude: '',
					longitude: '',
					iconPath: '../../static/images/contact-usl-icon2.png'
				}],
				submitData:{
					mainImg:[],
					
				}
			}
		},
		
		onLoad(options) {
			const self = this;
			self.id = options.id;
			self.$Utils.loadAll(['getLocation'], self);
		},
		
		methods: {
			
			getLocation(){
				const self = this;
				uni.getLocation({
				    type: 'wgs84',
				    success: function (res) {
						self.latitude = res.latitude;
						self.longitude = res.longitude;
				        self.covers[0].latitude = res.latitude;
						self.covers[0].longitude = res.longitude
				    }
				});
				self.$Utils.finishFunc('getLocation');
			},
			
			routineUpdate() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getStaffToken';
				postData.searchItem = {
					id:self.id,
					type:3
				};
				postData.data = {};
				postData.data = self.$Utils.cloneForm(self.submitData);
				postData.data.arrive_time = Date.parse(new Date())/1000;
				postData.data.latitude = self.latitude;
				postData.data.longitude = self.longitude;
				const callback = (data) => {				
					if (data.solely_code == 100000) {					
						self.$Utils.showToast('更新成功', 'none', 1000)
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
				self.$apis.routineUpdate(postData, callback);
			},
			
			submit() {
				const self = this;
				uni.setStorageSync('canClick', false);
				const pass = self.$Utils.checkComplete(self.submitData);
				console.log('pass', pass);
				console.log('self.submitData',self.submitData)
				if (pass) {	
					self.routineUpdate();
				} else {
					uni.setStorageSync('canClick', true);
					self.$Utils.showToast('请拍照上传', 'none')
				};
			},
			
			upLoadImg(type) {
				const self = this;			
				
				const callback = (res) => {
					console.log('res', res)
					if (res.solely_code == 100000) {
						self.submitData[type] = [];
						self.submitData[type].push({url:res.info.url,type:'image'})
						console.log(self.submitData)
					} else {
						self.$Utils.showToast('网络故障', 'none')
					}
				};				
				uni.chooseImage({
					count: 1,
					sourceType:['camera'],
					success: function(res) {
						console.log(res);
						var tempFilePaths = res.tempFilePaths[0];
						var file = res.tempFiles[0];
						var obj = res.tempFiles[0].path.lastIndexOf(".");
						var ext = res.tempFiles[0].path.substr(obj+1);
						console.log(callback)
						self.$Utils.uploadFile(tempFilePaths, 'file', {
							tokenFuncName: 'getStaffToken',ext:ext,md5:'md5',totalSize:file.size,start:0,chunkSize:file.size,originName:'headImg'
						}, callback)
					},
					fail: function(err) {
						uni.hideLoading();
					},			
				})			
			},
			
			
		}
	};
</script>

<style>
	page{height: 100%;box-sizing: border-box;}
	.backBtn{width: 20rpx;height: 36rpx;position: fixed;top: 70rpx;left: 28rpx; z-index: 10;}
	.mapBox{}
	
	.camera{width: 100%;height: 300rpx;}
	.camera .btn{width: 212rpx;height: 142rpx;}
</style>