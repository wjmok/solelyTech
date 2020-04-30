<template>
	<view>
		
		<view class="goOut mglr4">
			<view class="item flexRowBetween" v-for="(item,index) in mainData" :key="index">
				<view class="fixIcon"><image :src="item.behavior==1?'../../static/images/to-go-outl-img1.png':'../../static/images/to-go-outl-img.png'" mode=""></image></view>
				<view class="infor" @click="Router.navigateTo({route:{path:'/pages/staffUser-goOutDetail/staffUser-goOutDetail?id='+$event.currentTarget.dataset.id}})">
					<view class="flex row"><span class="title">缘由：</span>{{item.content}}</view>
					<view class="flex row"><span class="title">起始时间：</span>{{item.start_time>0?Utils.timeto(item.start_time*1000,'ymd-hms'):'-------'}}</view>
					<view class="flex row"><span class="title">到达时间：</span>{{item.arrive_time>0?Utils.timeto(item.arrive_time*1000,'ymd-hms'):'-------'}}</view>
					<view class="flex row"><span class="title">返程时间：</span>{{item.back_time>0?Utils.timeto(item.back_time*1000,'ymd-hms'):'-------'}}</view>
					<view class="flex row"><span class="title">结束时间：</span>{{item.end_time>0?Utils.timeto(item.end_time*1000,'ymd-hms'):'-------'}}</view>
				</view>
				<view class="arriveBtn fs16 ftw" v-if="item.start_time>0&&item.arrive_time==0" :data-id="item.id" @click="Router.navigateTo({route:{path:'/pages/staffUser-goOut-Arrive/staffUser-goOut-Arrive?id='+$event.currentTarget.dataset.id}})">到达</view>
				<view class="arriveBtn fs16 ftw" v-if="item.arrive_time>0&&item.back_time==0" @click="getLocation('back',index)">返程</view>
				<view class="arriveBtn fs16 ftw" v-if="item.back_time>0&&item.type!=3" @click="getLocation('end',index)">结束</view>
			</view>
			
		</view>
		
		<view class="R-fixIcon"  @click="Router.navigateTo({route:{path:'/pages/staffUser-goOutMsg/staffUser-goOutMsg'}})"><image src="../../static/images/to-go-outl-icon.png" mode=""></image></view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				mainData:[],
				Utils:this.$Utils,
			}
		},
		
		onLoad(options) {
			const self = this;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
		},
		
		onReachBottom() {
			console.log('onReachBottom')
			const self = this;
			if (!self.isLoadAll && uni.getStorageSync('loadAllArray')) {
				self.paginate.currentPage++;
				self.getMainData()
			};
		},
		
		onShow() {
			const self = this;
			self.mainData = [];
			self.$Utils.loadAll(['getMainData'], self);	
		},
		
		methods: {
			
			getLocation(type,index){
				const self = this;
				uni.getLocation({
				    type: 'wgs84',
				    success: function (res) {
						self.latitude = res.latitude;
						self.longitude = res.longitude;
						self.routineUpdate(type,index)
				    }
				});
				self.$Utils.finishFunc('getLocation');
			},
			
			routineUpdate(type,index) {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getStaffToken';
				postData.searchItem = {
					id:self.mainData[index].id,
					type:3
				};
				postData.data = {
					latitude:self.latitude,
					longitude:self.longitude
				};
				if(type=='back'){
					postData.data.back_time = Date.parse(new Date())/1000;
				}else if(type=='end'){
					postData.data.end_time = Date.parse(new Date())/1000;
				};
				const callback = (data) => {				
					if (data.solely_code == 100000) {					
						self.$Utils.showToast('更新成功', 'none', 1000)
						setTimeout(function() {
							self.getMainData(true)
						}, 1000);
					} else {
						uni.setStorageSync('canClick', true);
						self.$Utils.showToast(data.msg, 'none', 1000)
					}	
				};
				self.$apis.routineUpdate(postData, callback);
			},
			
			getMainData(isNew) {
				const self = this;
				if (isNew) {
					self.mainData = [];
					self.paginate = {
						count: 0,
						currentPage: 1,
						pagesize: 10,
						is_page: true,
					}
				};
				const postData = {};
				postData.tokenFuncName = 'getStaffToken';
				postData.paginate = self.$Utils.cloneForm(self.paginate);
				postData.searchItem = {
					thirdapp_id: 22,
					type:3
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData, res.info.data);
					}
					self.$Utils.finishFunc('getMainData');
			
				};
				self.$apis.routineGet(postData, callback);
			},
		}
	};
</script>

<style>
	page{background-color: #F5F5F5;}
	
	.R-fixIcon{width: 110rpx;height: 110rpx;position: fixed;bottom:30%;right: 30rpx;z-index: 66;}
	
	.goOut .item{background-color: #fff;height: 364rpx;box-sizing: border-box;border-radius: 10rpx;overflow: hidden;margin-top: 30rpx;padding: 30rpx;position: relative;}
	.goOut .item .fixIcon{width: 70rpx;height: 64rpx;position: absolute;top: 0;right: 0;}
	.goOut .item .infor{width: 70%;}
	.goOut .item .row{margin-bottom: 26rpx;}
	.goOut .item .row:last-child{margin-bottom: 0;}
	.goOut .item .row .title{width: 160rpx;font-size: 26rpx;color: #666;}
	.arriveBtn{width: 180rpx;height: 76rpx;line-height: 76rpx;border-radius: 40rpx;text-align: center;color: #fff;background-image:linear-gradient(to bottom,#49e3de,#2995e1);}
</style>