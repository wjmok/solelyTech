<template>
	<view>
		
		<view class="system flexRowBetween mglr4">
			<view class="item flex" v-for="(item,index) in mainData" :data-id="item.id"
			@click="Router.navigateTo({route:{path:'/pages/staffUser-systemDetail/staffUser-systemDetail?id='+$event.currentTarget.dataset.id}})">
				<view class="icon"><image :src="item.mainImg&&item.mainImg[0]?item.mainImg[0].url:''" mode=""></image></view>
				<view class="tit">{{item.title}}</view>
			</view>
			<!-- <view class="item flex" @click="Router.navigateTo({route:{path:'/pages/staffUser-systemDetail/staffUser-systemDetail'}})">
				<view class="icon"><image src="../../static/images/provisionsl-icon1.png" mode=""></image></view>
				<view class="tit">薪资制度</view>
			</view>
			<view class="item flex" @click="Router.navigateTo({route:{path:'/pages/staffUser-systemDetail/staffUser-systemDetail'}})">
				<view class="icon"><image src="../../static/images/provisionsl-icon2.png" mode=""></image></view>
				<view class="tit">年假制度</view>
			</view>
			<view class="item flex" @click="Router.navigateTo({route:{path:'/pages/staffUser-systemDetail/staffUser-systemDetail'}})">
				<view class="icon"><image src="../../static/images/provisionsl-icon3.png" mode=""></image></view>
				<view class="tit">日志制度</view>
			</view>
			<view class="item flex" @click="Router.navigateTo({route:{path:'/pages/staffUser-systemDetail/staffUser-systemDetail'}})">
				<view class="icon"><image src="../../static/images/provisionsl-icon4.png" mode=""></image></view>
				<view class="tit">请假制度</view>
			</view>
			<view class="item flex" @click="Router.navigateTo({route:{path:'/pages/staffUser-systemDetail/staffUser-systemDetail'}})">
				<view class="icon"><image src="../../static/images/provisionsl-icon5.png" mode=""></image></view>
				<view class="tit">迟到制度</view>
			</view> -->
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
							title: ['in', ['公司规定']],
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
	page{padding-bottom: 60rpx;}
	.system{flex-wrap: wrap;}
	.system .item{width: 345rpx;height: 160rpx;box-shadow: 0 0 12rpx rgba(0,0,0,0.1);box-sizing: border-box;padding: 30rpx 40rpx;margin-top: 30rpx;}
	.system .item .icon{width: 108rpx;height: 109rpx;margin-right: 20rpx;}
</style>
