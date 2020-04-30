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
			self.url = options.url;
			// self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
			
		}
	};
</script>

<style>
	
	.caseDetail image{width: 100%;}
</style>
