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
			<text class="uni-body">时间：{{item.time}}</text></br>
			<text class="uni-body">备注：{{item.remark}}</text>
		</uni-card>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				adviceList: [{
					name: "彭老师",
					content: "定时定期测血压",
					time : "2022-08-22 13:31:00",
					remark:''
				}]
			}
		},
		methods: {
			gotoadd() {
				console.log("111")
				uni.navigateTo({
				  url:'/pages/healthTreatment/doctorAdvice/add'
				})
			}
		}
	}
</script>

<style>

</style>
