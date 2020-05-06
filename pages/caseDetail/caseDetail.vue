<template>
	<view>
		<web-view  :src="url"></web-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				url:''
			}
		},
		onLoad(options) {
			const self = this;
			self.url = 'https://www.solelycloud.com/apinew/public/index.php/api/v1/Project/Solely/urlGetGet?getUrl='+ options.url;
			console.log('self.url',self.url);
			// self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
			
		}
	};
</script>

<style>
	
	.caseDetail image{width: 100%;}
</style>
