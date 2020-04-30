<template>
	<view>

		<view class="myRowBetween pdlr4">
			<view class="item flexRowBetween">
				<view class="ll flex">
					<view class="icon">
						<image src="../../static/images/resumel-icon.png" mode=""></image>
					</view>
					<view>姓名</view>
				</view>
				<view class="rr">
					<input type="text" v-model="submitData.title" placeholder="请输入" placeholder-class="placeholder" />
				</view>
			</view>
			<view class="item flexRowBetween">
				<view class="ll flex">
					<view class="icon">
						<image src="../../static/images/resumel-icon1.png" mode=""></image>
					</view>
					<view>电话</view>
				</view>
				<view class="rr">
					<input type="number" maxlength="11" v-model="submitData.phone" placeholder="请输入" placeholder-class="placeholder" />
				</view>
			</view>
			<view class="item flexRowBetween">
				<view class="ll flex">
					<view class="icon">
						<image src="../../static/images/resumel-icon2.png" mode=""></image>
					</view>
					<view>性别</view>
				</view>
				<view class="rr flexEnd">
					<view class="flex" @click="sexCurrChange('1')">
						<image class="seltIcon" :src="sexCurr==1?'../../static/images/resumel-icon12.png':'../../static/images/resumel-icon13.png'"
						 mode="">

						</image>男
					</view>
					<view class="flex" @click="sexCurrChange('2')" style="margin-left: 100rpx;">
						<image class="seltIcon" :src="sexCurr==2?'../../static/images/resumel-icon12.png':'../../static/images/resumel-icon13.png'"
						 mode="">

						</image>女
					</view>
				</view>
			</view>
			<view class="item flexRowBetween">
				<view class="ll flex">
					<view class="icon">
						<image src="../../static/images/resumel-icon3.png" mode=""></image>
					</view>
					<view>投递来源</view>
				</view>
				<view class="rr flexEnd" style="flex-wrap: wrap;">
					<view class="flex sourceSelt" @click="sourceChange(index)" v-for="(item,index) in sourceData" :key="index">
						<image class="seltIcon" :src="sourceCurr==index?'../../static/images/resumel-icon12.png':'../../static/images/resumel-icon13.png'"
						 mode=""></image>{{item}}
					</view>
				</view>
			</view>
			<view class="item flexRowBetween">
				<view class="ll flex">
					<view class="icon">
						<image src="../../static/images/resumel-icon4.png" mode=""></image>
					</view>
					<view>学历</view>
				</view>
				<view class="rr">
					<picker mode="selector" :range="educationData" @change="educationChange">
						<view class="flexEnd" :style="submitData.education==''?'color:#999':''">{{submitData.education!=''?submitData.education:'请选择'}}
							<image class="arrowR" src="../../static/images/0-icon.png" mode=""></image>
						</view>
					</picker>
					<!-- <input type="text" value="" placeholder="请输入" placeholder-class="placeholder" /> -->
				</view>
			</view>
			<view class="item flexRowBetween">
				<view class="ll flex">
					<view class="icon">
						<image src="../../static/images/resumel-icon5.png" mode=""></image>
					</view>
					<view>毕业院校及专业</view>
				</view>
				<view class="rr">
					<input type="text" v-model="submitData.college" placeholder="请输入" placeholder-class="placeholder" />
				</view>
			</view>
			<view class="item flexRowBetween">
				<view class="ll flex">
					<view class="icon">
						<image src="../../static/images/resumel-icon6.png" mode=""></image>
					</view>
					<view>投递职位</view>
				</view>
				<view class="rr">
					<picker mode="selector" :range="positionData" range-key="title" @change="positionChange">
						<view class="flexEnd" :style="!positionData[positionIndex].title?'color:#999':''">{{positionData[positionIndex]?positionData[positionIndex].title:'请选择'}}
							<image class="arrowR" src="../../static/images/0-icon.png" mode=""></image>
						</view>
					</picker>
				</view>
			</view>
			<view class="item flexRowBetween">
				<view class="ll flex">
					<view class="icon">
						<image src="../../static/images/resumel-icon7.png" mode=""></image>
					</view>
					<view>出生日期</view>
				</view>
				<view class="rr flexEnd">
					<picker mode="date" @change="bindDateChange">
						<view class="rr flexEnd">
							<view class="dateInput" style="width: 90rpx;">
								<input type="text" name="year" v-model="birth[0]" disabled="true" placeholder-class="placeholder" /></view>
							<view>年</view>
							<view class="dateInput">
								<input type="text" name="moths" v-model="birth[1]" disabled="true" placeholder-class="placeholder" /></view>
							<view>月</view>
							<view class="dateInput">
								<input type="text" name="day" v-model="birth[2]" disabled="true" placeholder-class="placeholder" /></view>
							<view>日</view>
						</view>
					</picker>
				</view>
			</view>
			<view class="item">
				<view class="flex ll">
					<view class="icon">
						<image src="../../static/images/resumel-icon8.png" mode=""></image>
					</view>
					<view>工作经历</view>
				</view>
				<view class="pdt10">
					<textarea style="border-color: #d4d4d4;height: 300rpx;" v-model="submitData.content" placeholder="请输入"
					 placeholder-class="placeholder" />
					</view>
			</view>
			<view class="item">
				<view class="flex ll">
					<view class="icon"><image src="../../static/images/resumel-icon8.png" mode=""></image></view>
					<view>上传照片</view>
				</view>
				<view class="pdt10 upLoadBtn" @click="upLoadImg('mainImg')" v-if="submitData.mainImg.length==0">
					<image src="../../static/images/resumel-icon14.png" mode=""></image>
				</view>
				<view class="pdt10 upImg flex" v-if="submitData.mainImg.length>0">
					<view class="lis"><image :src="submitData.mainImg&&submitData.mainImg[0]?submitData.mainImg[0].url:''" mode=""></image></view>
				</view>
			</view>
		</view>
		
		<view class="submitbtn" style="padding: 150rpx 0 60rpx 0;">
			<button class="btn" open-type="getUserInfo"  @getuserinfo="Utils.stopMultiClick(submit)">提交</button>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				Utils:this.$Utils,
				sexCurr:1,
				index:1,
				sourceCurr:0,
				sourceData:['智联','公司邀约','BOSS直聘'],
				submitData: {
					title: '',
					phone: '',
					passage_array: '',
					gender: '1',
					mainImg: [],
					content: '',
					relation_id: '',
					/* class:'' */
					education:'',
					origin:'',
					college:'',
				},
				urlSet:[],
				educationData:['硕士','本科','大专','高中'],
				positionIndex:-1,
				positionData:[],
				birth:[]
			}
		},
		
		
		
		onLoad(options) {
			const self = this;
			if(options.id){
				self.id = options.id;
				self.submitData.relation_id = self.id
			};
			self.$Utils.loadAll(['getMainData'], self);
		},
		
		methods: {
			
			educationChange(e){
				const self = this;
				self.submitData.education = self.educationData[e.detail.value]
			},
			
			
			
			getMainData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
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
						self.positionData.push.apply(self.positionData, res.info.data);
						for (var i = 0; i < self.positionData.length; i++) {
							if(self.positionData[i].id==self.id){
								self.positionIndex = i
							}
						}
					};
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.articleGet(postData, callback);
			},
			
			submit() {
				const self = this;
				uni.setStorageSync('canClick', false);
				var newObject = self.$Utils.cloneForm(self.submitData);
				const pass = self.$Utils.checkComplete(newObject);
				console.log('pass', pass);
				console.log('self.submitData',self.submitData)
				if (pass) {	
					const callback = (user, res) => {
						console.log(user)
						self.resumeAdd();
					};
					self.$Utils.getAuthSetting(callback);	
				} else {
					uni.setStorageSync('canClick', true);
					self.$Utils.showToast('请补全信息', 'none')
				};
			},
			
			resumeAdd() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.data = self.$Utils.cloneForm(self.submitData)
				const callback = (data) => {				
					if (data.solely_code == 100000) {					
						self.$Utils.showToast('投递成功', 'none', 1000)
						setTimeout(function() {
							uni.navigateBack({
								delta:1
							})
						}, 1000);
					} else {
						uni.setStorageSync('canClick', true);
						self.$Utils.showToast(data.msg, 'none', 1000)
					}	
				};
				self.$apis.resumeAdd(postData, callback);
			},
			
			
			upLoadImg(type) {
				const self = this;			
				
				const callback = (res) => {
					console.log('res', res)
					if (res.solely_code == 100000) {
						self.submitData[type] = [];
						self.submitData[type].push({url:res.info.url,type:'image'})
						console.log(self.submitData)
					} else {
						self.$Utils.showToast('网络故障', 'none')
					}
				};				
				uni.chooseImage({
					count: 1,
					success: function(res) {
						console.log(res);
						var tempFilePaths = res.tempFilePaths[0];
						var file = res.tempFiles[0];
						var obj = res.tempFiles[0].path.lastIndexOf(".");
						var ext = res.tempFiles[0].path.substr(obj+1);
						console.log(callback)
						self.$Utils.uploadFile(tempFilePaths, 'file', {
							tokenFuncName: 'getProjectToken',ext:ext,md5:'md5',totalSize:file.size,start:0,chunkSize:file.size,originName:'headImg'
						}, callback)
					},
					fail: function(err) {
						uni.hideLoading();
					},			
				})			
			},
			
			bindDateChange(e) {
				const self = this;
				console.log('picker发送选择改变，携带值为', e.detail.value);
				self.birth = e.detail.value.split("-");
				console.log(self.submitData.passage_array)
				self.submitData.passage_array = new Date(self.birth.join("-")).getTime();
			},
			
			positionChange(e) {
				const self = this;
				self.positionIndex = e.detail.value;
				self.submitData.relation_id = self.positionData[e.detail.value].id;
			},
			
			sexCurrChange(sexCurr){
				const self = this;
				if(sexCurr!=self.sexCurr){
					self.sexCurr = sexCurr;
					self.submitData.gender = self.sexCurr
				}
			},
			
			sourceChange(index){
				const self = this;
				self.sourceCurr = index;
				self.submitData.origin = self.sourceCurr+1
			},
			
			
		}
	};
</script>

<style>
	@import "../../assets/style/editInfor.css";
	page{padding-bottom: 60rpx;}
	
	.myRowBetween .item .ll{width: auto;}
	.myRowBetween .item .rr{width: auto;}
	.myRowBetween .ll .icon{width: 28rpx;height: 28rpx;margin-right: 10rpx;}
	.seltIcon{width: 32rpx;height: 32rpx;margin-right: 10rpx;}
	.sourceSelt{margin-left: 50rpx;}
	.sourceSelt:first-child{margin-left: 0;}
	
	.dateInput{width: 75rpx;}
	.myRowBetween .item .dateInput input{text-align: center;line-height: 40rpx;}
	.upLoadBtn{width: 120rpx;height: 120rpx;}
	
	.upImg{flex-wrap: wrap;}
	.upImg .lis{width: 162rpx;height: 162rpx;margin: 0 20rpx 20rpx 0;}
	.upImg .lis:nth-of-type(4n){margin-right: 0;}
</style>
