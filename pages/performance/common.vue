<template>
	<view>
		<z-nav-bar backState="2000" title="绩效"></z-nav-bar>
		<view class="u-demo-block">
			<u-swiper
				:list="wisperImage"
				indicator
				indicatorMode="line"
				circular
				height="150"
			></u-swiper>
		</view>
		<u-cell-group>
			<u-cell size="large" class="message" icon="../../static/icon/integral/col.png" url="/pages/mine/myPoints" title="积分"></u-cell>
			<u-cell size="large" class="message" icon="../../static/icon/integral/balance.png" url="/pages/mine/myComment" title="余额"></u-cell>
			<u-cell size="large" class="message" icon="../../static/icon/integral/order.png" url="/pages/mine/order" title="订单"></u-cell>
		</u-cell-group>
		<u-toast ref="uToast"></u-toast>
		<z-navigation></z-navigation>
	</view>
</template>

<script>
	import { wisperImage } from "../../static/js/performance/staticData";
	export default {
		data() {
			return {
				wisperImage,
			}
		},
		methods: { 
			click(url) {
				if(url === '') {
					this.$refs.uToast.default('开发中...')
				}
				uni.navigateTo({
					url: url
				});
			},
		}
	}
</script>

<style>

</style>
