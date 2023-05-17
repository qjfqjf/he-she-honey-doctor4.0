<template>
	<view>
		<z-nav-bar  title="医疗管理"></z-nav-bar>
		<public-module></public-module>
		<u-gap
			height="10"
		></u-gap>
		<u-cell-group>
			<u-cell size="large" class="message" url="/pages/healthTreatment/medicalTreatment/followUp" title="随访" isLink></u-cell>
			<u-cell size="large" class="message" url="" title="转诊" isLink></u-cell>	
			<u-cell size="large" class="message" url="/pages/healthTreatment/medicalTreatment/consultation" title="会诊" isLink></u-cell>
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
