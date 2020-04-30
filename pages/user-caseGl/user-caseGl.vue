<template>
	<view>
		
		<view class="caseGl mglr4">
			<view class="item flexRowBetween" v-for="(item,index) in mainData" :key="index" :data-id="item.id"
			 @click="Router.navigateTo({route:{path:'/pages/user-caseGlDetail/user-caseGlDetail?id='+$event.currentTarget.dataset.id}})">
				<view class="infor">
					<view class="fs12 color9">项目编号：{{item.project_no}}</view>
					<view class="flex row">
						<view class="icon"><image src="../../static/images/projectl-icon1.png" mode=""></image></view>
						<view><span class="mgr10 fs13 color6">合同编号：</span>缺少字段中</view>
					</view>
					<view class="flex row">
						<view class="icon"><image src="../../static/images/projectl-icon2.png" mode=""></image></view>
						<view><span class="mgr10 fs13 color6">项目名称：</span>{{item.name}}</view>
					</view>
					<view class="flex row">
						<view class="icon"><image src="../../static/images/projectl-icon7.png" mode=""></image></view>
						<view v-if="item.sign_status==0"><span class="mgr10 fs13 color6">项目状态：</span>立项中</view>
						<view v-if="item.sign_status==1"><span class="mgr10 fs13 color6">项目状态：</span>开发中</view>
						<view v-if="item.sign_status==2"><span class="mgr10 fs13 color6">项目状态：</span>交付测试</view>
						<view v-if="item.sign_status==3"><span class="mgr10 fs13 color6">项目状态：</span>已交接</view>
						<view v-if="item.sign_status==4"><span class="mgr10 fs13 color6">项目状态：</span>已完结</view>
						<view v-if="item.sign_status==5"><span class="mgr10 fs13 color6">项目状态：</span>烂尾</view>
					</view>
				</view>
				<view class="arrowR"><image src="../../static/images/0-icon.png" mode=""></image></view>
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
				mainData:[]
			}
		},
		
		onLoad(options) {
			const self = this;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			self.$Utils.loadAll(['getUserInfoData'], self);	
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
			
			getUserInfoData(){
			    var self = this;
			    var postData = {};
				postData.tokenFuncName = 'getProjectToken';
			    postData.searchItem = {
					thirdapp_id:2
				};
			    var callback = function(res){
			        if(res.info.data.length>0&&res.info.data[0]){
						self.userInfoData  = res.info.data[0];
						if(self.userInfoData.phone!=''){
							self.getMainData()
						}else{
							self.$Utils.finishFunc('getUserInfoData');
							uni.showModal({
								title:'提示',
								content:'请先绑定您的手机号，以便匹配您的项目。是否立即去绑定',
								success(res) {
									if(res.confirm){
										self.Router.redirectTo({route:{path:'/pages/userInfor/userInfor'}})
									}else{
										uni.navigateBack({
											delta:1
										})
									}
								}
							})
						}
			        };    
			    };
				self.$apis.userInfoGet(postData, callback);
			},
			
			getMainData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.paginate = self.$Utils.cloneForm(self.paginate);
				postData.searchItem = {
					thirdapp_id:22,
					phone:self.userInfoData.phone
				};
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.mainData.push.apply(self.mainData,res.info.data);
					};
					self.$Utils.finishFunc('getUserInfoData');
				};
				self.$apis.projectGet(postData, callback);
			},
		}
	};
</script>

<style>
	page{padding-bottom: 60rpx;background-color: #F5F5F5;}	
	.caseGl .item{background-color: #fff;height: 280rpx;box-sizing: border-box;border-radius: 10rpx;overflow: hidden;margin-top: 30rpx;padding: 30rpx;}
	.caseGl .item .infor{width: 90%;}
	.caseGl .item .infor .icon{width: 34rpx;height: 34rpx;margin-right: 10rpx;}
	.caseGl .item .row{margin-top: 20rpx;}
</style>