<template>
	<view>
		<z-nav-bar title="随访">
			<view slot="right" class="p-2">
			  <image style="width: 40rpx;height: 40rpx;" src="/static/icon/healthTreatment/add.png" @click="gotoadd()"></image>
			</view>
		</z-nav-bar>
		<public-module></public-module>
		<uni-card :is-shadow="false" v-for="(item, index) in adviceList">
			<text class="uni-body">会员：{{item.name}}</text></br>
			<text class="uni-body">类型：{{item.type}}</text></br>
			<text class="uni-body">内容：{{item.content}}</text></br>
			<text class="uni-body">时间：{{item.time}}</text>
			<u-button type="error" text="删除" click="delete" style="width: 100upx;margin-left: 260px;"></u-button>
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
					type:''
				}]
			}
		},
		methods: {
			delete() {
				
			},
			gotoadd() {
				console.log("111")
				uni.navigateTo({
				  url:'/pages/healthTreatment/medicalTreatment/add'
				})
			}
		}
	}
</script>

<style>

</style>
