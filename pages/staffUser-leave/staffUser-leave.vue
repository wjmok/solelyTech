<template>
	<view>
		
		<view class="leaveList mglr4  fs13">
			<view class="item flexRowBetween" v-for="(item,index) in mainData"  :data-id="item.id"
			@click="Router.navigateTo({route:{path:'/pages/staffUser-leaveDetail/staffUser-leaveDetail?id='+$event.currentTarget.dataset.id}})">
				<view class="infor" style="width: 75%">
					<view>申请时间：{{item.create_time}}</view>
					<view class="mgt10">请假事由：{{item.content}}</view>
				</view>
				<view class="rr fs12" style="width:25%">
					<view class="pubColor mgb5 flexEnd" v-if="item.num==0">状态：审核中</view>
					<view class="pubColor mgb5 flexEnd" v-if="item.num==1">状态：已审核</view>
					<view class="pubColor mgb5 flexEnd" v-if="item.num==2">状态：已拒绝</view>
					<view class="flexEnd"><image class="arrowR" src="../../static/images/0-icon.png" mode=""></image></view>
				</view>
			</view>
		</view>
		<view class="R-fixIcon"  @click="Router.navigateTo({route:{path:'/pages/staffUser-leaveAdd/staffUser-leaveAdd'}})"><image src="../../static/images/to-go-outl-icon.png" mode=""></image></view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				mainData:[],
			}
		},
		
		onLoad(options) {
			const self = this;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			self.$Utils.loadAll(['getMainData'], self);	
		},
		
		onReachBottom() {
			console.log('onReachBottom')
			const self = this;
			if (!self.isLoadAll && uni.getStorageSync('loadAllArray')) {
				self.paginate.currentPage++;
				self.getMainData()
			};
		},
		
		methods: {
			
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
					type:4
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
	page{padding-bottom: 60rpx;background-color: #F5F5F5;}
	
	.R-fixIcon{width: 110rpx;height: 110rpx;position: fixed;bottom:30%;right: 30rpx;z-index: 66;}
	
	.leaveList .item{background-color: #fff;height: 160rpx;box-sizing: border-box;border-radius: 10rpx;overflow: hidden;margin-top: 30rpx;padding:30rpx; align-items:flex-start;}
	.leaveList .item .infor{width: 55%;}
	.leaveList .item .rr{width: 45%;}
</style>