<template>
	<view>
		<z-nav-bar title="医嘱管理">
			<view slot="right" class="p-2">
			  <image style="width: 40rpx;height: 40rpx;" src="/static/icon/healthTreatment/add.png" @click="gotoadd()"></image>
			</view>
		</z-nav-bar>
		<public-module></public-module>
		<uni-card :is-shadow="false" v-for="(item, index) in adviceList">
			<text class="uni-body">{{item.name}}</text></br>
			<text class="uni-body">内容：{{item.content}}</text></br>
			<text class="uni-body">时间：{{item.date}}</text></br>
			<text class="uni-body">开始时间：{{item.start_date}}</text></br>
			<text class="uni-body">结束时间：{{item.end_date}}</text></br>
			<text class="uni-body">备注：{{item.remarks}}</text>
		</uni-card>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				adviceList: []
			}
		},
		onLoad: function (option) {
			this.getDoctorAdvice()
		},
		methods: {
			getDoctorAdvice(){
				this.$http.post('/advice/index',{
					// type:1
				}).then((res)=>{
				res.data.data.forEach(element => {
					const newData = {};
					newData.name = element.fullname;
					newData.content = element.content;
					newData.date = element.createtime;
					newData.start_date = element.start_date;
					newData.end_date = element.end_date;
					newData.remarks = element.remarks;
					this.adviceList.push(newData);
				});
				})
			},
			// 跳转至添加医嘱页面
			gotoadd() {
				uni.navigateTo({
				  url:'/pages/healthTreatment/doctorAdvice/add'
				})
			}
		}
	}
</script>

<style>

</style>
