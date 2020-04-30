<template>
	<view>
		
		<view class="pdlr4 pdt20 pdb20">
			<view class="fs20 mgb15">{{mainData.title}}</view>
			<view class="flex fs13"><span class="red">{{mainData.small_title}}</span>{{item.description}}</view>
		</view>
		<view class="f5H10"></view>
		
		<view class="pdlr4">
			<view class="fs16 ftw mgb10 pdt20">职位描述</view>
			<!-- <view class="flex">
				<view class="jobLable fs13">会计助理</view>
			</view> -->
			<view class="content ql-editor" style="padding:0;"
			v-html="mainData.content">
			</view>
		</view>
		
		<view class="submitbtn" style="padding: 150rpx 0 100rpx 0;">
			<view class="btn"  @click="Router.navigateTo({route:{path:'/pages/sendResumes/sendResumes?id='+id}})">投递简历</view>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				mainData:{},
				id:''
			}
		},
		
		onLoad(options) {
			const self = this;
			self.id = options.id;
			self.$Utils.loadAll(['getMainData'], self);
		},
		
		methods: {
			
			getMainData(){
			    var self = this;
			    var postData = {};
				postData.tokenFuncName = 'getProjectToken';
			    postData.searchItem = {
					id:self.id,
					thirdapp_id:22,
				};
			    var callback = function(res){
			        if(res.info.data.length>0&&res.info.data[0]){
						self.mainData  =res.info.data[0];
						const regex = new RegExp('<img', 'gi');
						self.mainData.content = self.mainData.content.replace(regex, `<img style="max-width: 100%;"`);
			        };    
					self.$Utils.finishFunc('getMainData');
			    };
				self.$apis.articleGet(postData, callback);
			},
		}
	};
</script>

<style>
	.jobLable{height: 60rpx;line-height: 58rpx;padding: 0 10px;border-radius: 36rpx;border: 1px solid #EEE;color: #666; margin: 0 20rpx 20rpx 0;}
	.xqInfor view{margin-bottom: 10rpx;}
</style>
