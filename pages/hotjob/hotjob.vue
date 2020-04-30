<template>
	<view>
		
		<view class="">
			
			<view class="jobList">
				<view class="item" v-for="(item,index) in mainData" :key="index" :data-id="item.id"
				 @click="Router.navigateTo({route:{path:'/pages/hotjobDetail/hotjobDetail?id='+$event.currentTarget.dataset.id}})">
					<view class="flexRowBetween">
						<view class="tit fs13">{{item.title}}</view>
						<view class="pubColor">{{item.small_title}}</view>
					</view>
					<view class="flex lable color9">
						<view class="tt">{{item.description}}</view>
					</view>
					<view class="flex mgt15 color9 fs12">
						<view class="photo"><image src="../../static/images/positionl-img.png" mode=""></image></view>
						<view>纯粹科技</view>
					</view>
				</view>
			</view>
			
			<!-- 无数据 -->
			<view class="nodata" v-if="mainData.length==0"><image src="../../static/images/nodata.png" mode=""></image></view>
		</view>
		
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
				postData.tokenFuncName = 'getProjectToken';
				postData.paginate = self.$Utils.cloneForm(self.paginate);
				postData.getBefore = {
					article:{
						tableName:'Label',
						middleKey:'menu_id',
						key:'id',
						searchItem:{
							title: ['in', ['热招职位']],
						},
						condition:'in'
					}
				};
				postData.searchItem = {
					thirdapp_id: 22,
				};
				postData.order = {
					listorder: 'desc'
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData, res.info.data);
					}
					self.$Utils.finishFunc('getMainData');
			
				};
				self.$apis.articleGet(postData, callback);
			},
		}
	};
</script>

<style>
	/* @import "../../assets/style/navbar.css"; */
	page{background-color: #F5F5F5;}
	.jobList .item{margin-bottom: 20rpx;background: #fff;overflow: hidden;padding: 40rpx 2.666%;}
	.jobList .item .pic{width: 100%;height: 612rpx;}
	.jobList .item .tit{font-size: 28rpx;width: 75%;}
	.jobList .lable{margin-top: 20rpx;flex-wrap: wrap;}
	.jobList .lable .tt{font-size: 20rpx;line-height: 40rpx;padding: 0 20rpx;border-radius: 6rpx;background: #effeff;margin-right: 30rpx;}
	.jobList .photo{width: 56rpx;height: 56rpx;border-radius: 50%;overflow: hidden;margin-right: 20rpx;}
</style>
