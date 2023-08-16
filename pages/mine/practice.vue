<template>
	<view>
		<z-nav-bar title="执业信息" bgColor="#ffffff"></z-nav-bar>
		<!-- 公共组件-每个页面必须引入 -->
		<public-module></public-module>
		<view class="create" v-if="this.type === 'add'">
			<u-cell-group :border="false" class="message" display="flex">
				<u-cell title="基本信息" titleStyle="font-weight: bold; font-size: 16px" :border="false"></u-cell>
				<u-cell size="large" title="头像" titleStyle="font-size: 14px">
					<u-avatar slot="value" :src="avatar"></u-avatar>
				</u-cell>
				<u-cell @click="showNameModal" titleStyle="font-size: 14px" size="large" icon="star-fill"
					:icon-style="iconStyle" title="姓名" :isLink="true">
					<text slot="value" class="u-slot-value"></text>
				</u-cell>
				<u-cell @click="showGenderModal" size="large" titleStyle="font-size: 14px" icon="star-fill"
					:icon-style="iconStyle" title="性别" :isLink="true">
					<text slot="value" class="u-slot-value"></text>
				</u-cell>
				<u-cell @click="showBirthModal" class="message" titleStyle="font-size: 14px" size="large"
					icon="star-fill" :icon-style="iconStyle" title="出生日期" :value="birth" :isLink="true">
					<text slot="value" class="u-slot-value"></text>
				</u-cell>
			</u-cell-group>
			<u-gap height="10"></u-gap>
			<u-cell-group :border="false" class="message">
				<u-cell size="large" title="身份信息" titleStyle="font-weight: bold;" :border="false"></u-cell>
				<u-cell @click="showIdCardNumberModel" size="large" title="身份证号" titleStyle="font-size: 14px"
					:isLink="true">
					<text slot="value" class="u-slot-value"></text>
				</u-cell>
				<u-cell size="large" icon="star-fill" :icon-style="iconStyle" title="亲属关系" titleStyle="font-size: 14px"
					:isLink="true" @click="showRelation = true">
					<text slot="value" class="u-slot-value"></text>
				</u-cell>
				<u-cell @click="showTelModel" size="large" icon="star-fill" :icon-style="iconStyle" title="手机号"
					titleStyle="font-size: 14px" :isLink="true">
					<text slot="value" class="u-slot-value"></text>
				</u-cell>
				<u-cell @click="showCodeModel" size="large" icon="star-fill" :icon-style="iconStyle" title="验证码"
					titleStyle="font-size: 14px" :isLink="true">
					<text slot="value" class="u-slot-value"></text>
				</u-cell>
			</u-cell-group>
			<u-gap height="10"></u-gap>
			<u-cell-group :border="false" class="message">
				<u-cell size="large" title="身体信息" titleStyle="font-weight: bold;" :border="false"></u-cell>
				<u-cell @click="showHeightModel" size="large" icon="star-fill" :icon-style="iconStyle" title="身高(cm)"
					titleStyle="font-size: 14px" :isLink="true">
					<text slot="value" class="u-slot-value"></text>
				</u-cell>
				<u-cell @click="showWeightModel" size="large" icon="star-fill" :icon-style="iconStyle" title="体重(kg)"
					titleStyle="font-size: 14px" :isLink="true">
					<text slot="value" class="u-slot-value"></text>
				</u-cell>
			</u-cell-group>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				nameValue: '',
				idCardNumberValue: '',
				telValue: '',
				codeValue: '',
				heightValue: '',
				weightValue: '',
				relationShip: '',
				gender: '',
				relationShipText: '',
				chooseDate: Number(new Date()),

				
			}
		}
	}
</script>

<style lang="scss">
	@import '@/style/mixin.scss';

	.message {
		background-color: #ffffff;
	}

	.u-slot-value {
		color: gray;
		font-size: 14px;
	}

	.form_but {
		background-color: rgb(32, 198, 162);
		color: #ffffff;
		border-radius: 50upx;
	}
</style>