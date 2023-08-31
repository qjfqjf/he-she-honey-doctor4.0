<template>
	<view>
		<z-nav-bar title="医嘱">
			<view slot="right" class="p-2" @click="save">
        	提交
      	</view>
		</z-nav-bar>
		<uni-card title="请填写医嘱内容" style="height: 350upx;">
			<u--textarea
				v-model="content"
				placeholder="请输入内容"
				border="null"
			></u--textarea>
		</uni-card>
		<uni-card title="请选择医嘱日期时间">
			<view class="example-body">
				<uni-datetime-picker type="datetime" v-model="datetimesingle" />
			</view>
		</uni-card>
		 <u-cell-group class="object">
		 		<u-cell title="请选择测量对象">
					<image
						slot="value"
						style="width: 40rpx;height: 40rpx;" 
						src="/static/icon/healthTreatment/add.png"
						@click="showObjectModel"
					></image>
				</u-cell>
		 </u-cell-group>
		<uni-card title="备注" style="height: 350upx;">
			<u--textarea
				v-model="remark"
				placeholder="请输入内容"
				border="null"
			></u--textarea>
		</uni-card>
		<u-action-sheet
			:show="showObject"
			:actions="actions"
			title="请选择测量对象"
			@close="showObject = false"
			@select="ObjectSelect"
		>
		</u-action-sheet>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				showObject: false,
				content: "",
				remark: "",
				datetimesingle: '',
				actions: [],
			}
		},
		methods: {
			save(){
				this.$http.post('/advice/save',{
					content: this.content,
					remarks:this.remark,
					start_date: this.datetimesingle,
					end_date: '',
					
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
			showObjectModel() {
				this.showObject = true;
			}
		}
	}
</script>

<style>
.object{
	width: 690upx; 
	margin: auto;
	background-color: #fff;
	border-radius: 14upx;
}
</style>
