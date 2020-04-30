<template>
	<view>
		<view class="userHead pr">
			<view class="headbj"><image src="../../static/images/about-img.png" mode=""></image></view>
			<view class="quitBtn" style="font-size: 25rpx;font-weight: bold;" @click="loginOff">退出</view>
			
			<view class="quitBtn" style="border: 1px solid #777777;border-radius: 30rpx;width: 50px;line-height: 25px;text-align: center;left:25rpx;" @click="Utils.stopMultiClick(scan)" v-if="routineData.length<2">{{routineData.length>0?'签退':'签到'}}</view>
			<view class="infor flexColumn">
				<view class="photo">
					<image :src="mainData.mainImg&&mainData.mainImg[0]?mainData.mainImg[0].url:''" mode=""></image>
				</view>
				<view class="fs13 mgt10">{{mainData.name}}</view>
			</view>
		</view>
		
		<view class="twoBox flex fs13 color3">
			<view class="item flexCenter" @click="showToast">
				<view>
					<view class="icon"><image src="../../static/images/employeesl-icon.png" mode=""></image></view>
					<view>简历管理</view>
				</view>
			</view>
			<view class="item flexCenter" @click="Router.navigateTo({route:{path:'/pages/staffUser-goOut/staffUser-goOut'}})">
				<view>
					<view class="icon"><image src="../../static/images/employeesl-icon1.png" mode=""></image></view>
					<view>外出登记</view>
				</view>
			</view>
			<view class="item flexCenter" @click="showToast">
				<view>
					<view class="icon"><image src="../../static/images/employeesl-icon2.png" mode=""></image></view>
					<view>项目管理</view>
				</view>
			</view>
			<view class="item flexCenter" @click="showToast">
				<view>
					<view class="icon"><image src="../../static/images/employeesl-icon3.png" mode=""></image></view>
					<view>推广客户</view>
				</view>
			</view>
			<view class="item flexCenter" @click="Router.navigateTo({route:{path:'/pages/staffUser-salary/staffUser-salary'}})">
				<view>
					<view class="icon"><image src="../../static/images/employeesl-icon4.png" mode=""></image></view>
					<view>我的薪资</view>
				</view>
			</view>
			<view class="item flexCenter" @click="Router.navigateTo({route:{path:'/pages/staffUser-system/staffUser-system'}})">
				<view>
					<view class="icon"><image src="../../static/images/employeesl-icon5.png" mode=""></image></view>
					<view>公司规定</view>
				</view>
			</view>
			<view class="item flexCenter" @click="Router.navigateTo({route:{path:'/pages/staffUser-leave/staffUser-leave'}})">
				<view>
					<view class="icon"><image src="../../static/images/employeesl-icon6.png" mode=""></image></view>
					<view>请假</view>
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
				mainData:{},
				routineData:[]
			}
		},
		
		onLoad() {
			const self = this;
			self.$Utils.loadAll(['getMainData','getRoutineData'], self);
		},
		
		methods: {
			
			
			getRoutineData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getStaffToken';
				postData.searchItem = {
					thirdapp_id: 22,
					type:2,
					create_time:['between',[new Date(new Date().toLocaleDateString()).getTime()/1000,new Date(new Date().toLocaleDateString()).getTime()/1000+86400]]
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.routineData = res.info.data
					}
					self.$Utils.finishFunc('getRoutineData');
				};
				self.$apis.routineGet(postData, callback);
			},
			
			getLocation(){
				const self = this;
				uni.getLocation({
				    type: 'wgs84',
				    success: function (res) {
						self.latitude = res.latitude;
						self.longitude = res.longitude;
						self.routineAdd()
				    }
				});
				self.$Utils.finishFunc('getLocation');
			},
			
			
			routineAdd() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getStaffToken';
				postData.check_token = uni.getStorageSync('user_token');
				postData.latitude = self.latitude;
				postData.longitude = self.longitude;
				postData.check =  self.code 
				postData.data = {
					type:2
				};
				const callback = (data) => {				
					if (data.solely_code == 100000) {	
						uni.setStorageSync('canClick', true);
						self.$Utils.showToast('操作成功', 'none', 1000)
						self.getRoutineData()
					} else {
						uni.setStorageSync('canClick', true);
						self.$Utils.showToast(data.msg, 'none', 1000)
					}	
				};
				self.$apis.routineAdd(postData, callback);
			},
			
			
			showToast(){
				const self = this;
				self.$Utils.showToast('功能开发中~','none')
			},
			
			getMainData(){
			    var self = this;
			    var postData = {};
				postData.tokenFuncName = 'getStaffToken';
			    postData.searchItem = {
					thirdapp_id:22
				};
			    var callback = function(res){
			        if(res.info.data.length>0&&res.info.data[0]){
						self.mainData  = res.info.data[0];
			        };    
					self.$Utils.finishFunc('getMainData');
			    };
				self.$apis.userInfoGet(postData, callback);
			},
			
			loginOff(){
				const self = this;
				uni.removeStorageSync('staff_info');
				uni.removeStorageSync('staff_token');
				self.Router.redirectTo({route:{path:'/pages/staffUser/staffUser'}})
			},
			
			scan(){
				const self = this;
				uni.setStorageSync('canClick', false);
				uni.scanCode({
				    success: function (res) {
				        console.log('条码类型：' + res.scanType);
				        console.log('条码内容：' + res.result);
						self.code =  res.result;
						self.getLocation()
				    }
				});
			},
		},
	};
</script>

<style>
	
	page{padding-bottom: 60rpx;background-color: #F5F5F5;}
	.headbj{width: 100%;height:400rpx;position: absolute;top: 0;right: 0;bottom: 0;left: 0;}
	.userHead{padding-top: 80rpx;height:400rpx;box-sizing: border-box;}
	.userHead .infor{position:relative ; z-index: 1;}
	.quitBtn{position: absolute;top: 30rpx;right: 30rpx;}
	
	
	.userHead .photo{width: 185rpx;height: 185rpx;padding: 14rpx;box-sizing: border-box;border: 1px solid rgba(255,255,255,0.5);border-radius: 50%;overflow: hidden;}
	.userHead .photo image{width: 100%;height: 100%;border-radius: 50%;box-sizing: border-box;border: 1px solid #fff;}
	
	.twoBox{flex-wrap:wrap ;}
	.twoBox .item{width: 33.33%;height: 250rpx;padding: 30rpx 0;box-sizing: border-box;border-right:1px solid #eee;border-bottom:1px solid #eee;background-color: #fff;}
	.twoBox .item .icon{width: 44rpx;height: 44rpx;display: block;margin: 0 auto 24rpx auto;}
	.twoBox .item .icon image{width: 100%;height: 100%;}
	/* .twoBox .item:nth-last-of-type(2),.twoBox .item:nth-last-of-type(1){border-bottom: 0;} */
</style>
