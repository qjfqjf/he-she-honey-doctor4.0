<template>
	<view>
		<z-nav-bar title="心理调试"></z-nav-bar>
		<u-gap
			height="10"
		></u-gap>
		<u-cell-group class="object">
			<u-cell title="请选择会员">
				<image
					slot="value"
					style="width: 40rpx;height: 40rpx;" 
					src="/static/icon/healthTreatment/add.png"
					@click="showObjectModel"
				></image>
			</u-cell>
		</u-cell-group>
		<uni-card title="请选择时间">
			<view class="example-body">
				<uni-datetime-picker type="datetime" v-model="datetime" />
			</view>
		</uni-card>
		<uni-card title="调试记录">
			<u-upload
				:fileList="fileList"
				@afterRead="afterRead"
				@delete="deletePic"
				name="1"
				multiple
				:maxCount="10"
			></u-upload>
			<u-divider></u-divider>
			<u--textarea
				v-model="describe"
				placeholder="调试记录描述"
				border="null"
			></u--textarea>
		</uni-card>
		<uni-card title="心理建议">
			<u-upload
				:fileList="fileList"
				@afterRead="afterRead"
				@delete="deletePic"
				name="1"
				multiple
				:maxCount="10"
			></u-upload>
			<u-divider></u-divider>
			<u--textarea
				v-model="describe"
				placeholder="心理建议描述"
				border="null"
			></u--textarea>
		</uni-card>
		<uni-card title="症状自述">
			<u-upload
				:fileList="fileList"
				@afterRead="afterRead"
				@delete="deletePic"
				name="1"
				multiple
				:maxCount="10"
			></u-upload>
			<u-divider></u-divider>
			<u--textarea
				v-model="describe"
				placeholder="症状自述描述"
				border="null"
			></u--textarea>
		</uni-card>
		<view class="d-flex j-center">
			<u-button
				text="保存"
				size="large"
				type="success"
				shape="circle"
				color="rgb(10, 185, 156)"
				style="width: 660rpx; height: 110rpx;"
			></u-button>
		</view>
		<u-action-sheet
			:show="showObject"
			:actions="actions"
			title="请选择测量会员"
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
				datetime:"",
				fileList: [],
				describe:"",
				actions:[],
			}
		},
		methods: {
			showObjectModel() {
				this.showObject = true;
			},
			// 删除图片
			deletePic(event) {
				this[`fileList${event.name}`].splice(event.index, 1)
			},
			// 新增图片
			async afterRead(event) {
				// 当设置 multiple 为 true 时, file 为数组格式，否则为对象格式
				let lists = [].concat(event.file)
				let fileListLen = this[`fileList${event.name}`].length
				lists.map((item) => {
					this[`fileList${event.name}`].push({
						...item,
						status: 'uploading',
						message: '上传中'
					})
				})
				for (let i = 0; i < lists.length; i++) {
					const result = await this.uploadFilePromise(lists[i].url)
					let item = this[`fileList${event.name}`][fileListLen]
					this[`fileList${event.name}`].splice(fileListLen, 1, Object.assign(item, {
						status: 'success',
						message: '',
						url: result
					}))
					fileListLen++
				}
			},
			uploadFilePromise(url) {
				return new Promise((resolve, reject) => {
					let a = uni.uploadFile({
						url: 'http://192.168.2.21:7001/upload', // 仅为示例，非真实的接口地址
						filePath: url,
						name: 'file',
						formData: {
							user: 'test'
						},
						success: (res) => {
							setTimeout(() => {
								resolve(res.data.data)
							}, 1000)
						}
					});
				})
			},
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
