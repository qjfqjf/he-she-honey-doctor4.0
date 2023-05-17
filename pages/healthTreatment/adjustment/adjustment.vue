<template>
	<view>
		<z-nav-bar  title="调理管理"></z-nav-bar>
		<public-module></public-module>
		<u-gap
			height="10"
		></u-gap>
		<u-cell-group>
			<u-cell size="large" class="message" url="/pages/healthTreatment/adjustment/adjust" title="调理管理" isLink></u-cell>
			<u-cell size="large" class="message" url="/pages/healthTreatment/adjustment/diet" title="饮食管理" isLink></u-cell>	
			<u-cell size="large" class="message" url="/pages/healthTreatment/adjustment/motion" title="运动管理" isLink></u-cell>
			<u-cell size="large" class="message" url="/pages/healthTreatment/adjustment/sleep" title="睡眠管理" isLink></u-cell>	
		</u-cell-group>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			
		}
	}
</script>

<style>
.message{
	background-color: #fff;
}
</style>
