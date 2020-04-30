<template>
	<view>
		
		<view class="xqInfor fs13  pdlr4 whiteBj">
			<view class="content ql-editor" style="padding:0;"
			v-html="mainData.content">
			</view>
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
						uni.setNavigationBarTitle({
							title:self.mainData.title
						});
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
	page{padding-bottom: 60rpx;background-color: #F5F5F5;}
	
	.xqInfor{padding: 30rpx 2.666%;}
	.xqInfor view{margin-bottom: 20rpx;line-height: 44rpx;}
</style>
