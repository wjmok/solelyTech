<template>
	<view>
		
		<view class="detailBanner">
			<image :src="mainData.bannerImg&&mainData.bannerImg[0]?mainData.bannerImg[0].url:''" mode=""></image>
		</view>
		
		<view class="mglr4 pdt15 xqInfor" >
			<view class="cont fs13">
				<view class="content ql-editor" style="padding:0;"
				v-html="mainData.content">
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
	page{padding-bottom:60rpx;}
	
	.detailBanner{width: 100%;height: 400rpx;box-sizing: border-box;overflow: hidden;}
	
	.xqInfor .cont{line-height: 44rpx;}
	.xqInfor .cont view{padding-bottom: 10rpx;}
	
	
</style>
