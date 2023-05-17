<template>
	<view>
		<z-nav-bar title="随访"></z-nav-bar>
		<uni-card title="请选择回访时间">
			<view class="example-body">
				<uni-datetime-picker v-model="datetimerange" type="datetimerange" rangeSeparator="至" />
			</view>
		</uni-card>
		<u-cell-group class="object">
			<u-cell title="请选择回访会员">
				<image
					slot="value"
					style="width: 40rpx;height: 40rpx;" 
					src="/static/icon/healthTreatment/add.png"
					@click="showObjectModel"
				></image>
			</u-cell>
		</u-cell-group>
		<uni-card title="请选择回访类型">
			<view class="chooseType">
				<u-button v-for="(item, index) in typeList" class="button" type="success" :plain="true" size="mini" shape="circle" click="chooseType(index)">{{ item.type }}</u-button>
			</view>
		</uni-card>
		<uni-card title="回访原因" style="height: 350upx;">
			<u--textarea
				v-model="reason"
				placeholder="请输入回访原因"
				border="null"
			></u--textarea>
		</uni-card>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				datetimerange: '',
				typeList: [{
					type: "视频随访",
				},{
					type: "电话随访",
				}],
				reason:"",
			}
		},
		methods: {
			chooseMedia() {
				this.type="视频随访"
			},
			choosePhone() {
				this.type="视频随访"
			},
		}
	}
</script>

<style>
	.chooseType{
		display: flex;
	}
	.button{
		width: 200upx;
		margin-right: 10upx;
	}
	.object{
		width: 690upx; 
		margin: auto;
		background-color: #fff;
		border-radius: 14upx;
	}
</style>
