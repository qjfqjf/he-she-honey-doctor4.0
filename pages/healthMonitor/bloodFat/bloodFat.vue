<template>
	<view class="content p-2">
		<z-nav-bar title="血脂">
			<view slot="right" class="p-2" @click="handleDevelop">预警规则</view>
		</z-nav-bar>
		<public-module></public-module>
		<HealthHeader :username="username" @myUser="handleMyUser"></HealthHeader>

		<view class="data d-flex j-sb flex-wrap" style="margin-top: 100rpx;">
			<view class="item d-flex flex-column a-center w-50" v-for="item in data" :key="item.unit">
				<view class="value">
					{{item.value||'--'}}
				</view>
				<view class="unit">
					{{item.unit}}
				</view>
			</view>

		</view>
		<TipInfo title="血脂趋势"></TipInfo>
		<u--text class="d-flex j-center mb-3" color="#01b09a"
			:text="deviceStatus===0?'设备状态：未连接':'设备状态：已连接'+'('+deviceId+')'"></u--text>
		<u-button class="mt-2" :color="btnColor" text="保存" @click="handleSaveHeat"></u-button>
		<view class="mb-3">

		</view>
		<u--text class="d-flex j-center" color="#20baa6" suffixIcon="arrow-right"
			iconStyle="font-size: 15px;color:#20baa6" text="查看监测历史" @click="handleDevelop">
		</u--text>
		<!-- <BottomNavigation page="bloodSUA/suaManualEntry"></BottomNavigation> -->
		<view class="tools d-flex j-sb mt-5 p-4">
			<view class="d-flex flex-column a-center" v-for="item in toolList" :key="item.title"
				@click="onPageJump(item.url)">
				<image :src="item.img" style="width: 100rpx; height: 100rpx;" mode="aspectFit"></image>
				<text class="mt-1">{{item.title}}</text>
			</view>
		</view>
		<u-toast ref="uToast"></u-toast>
	</view>
</template>

<script>
	import HealthHeader from "../components/healthHeader/HealthHeader.vue"
	import TipInfo from '../components/tipInfo/TipInfo.vue'
	import BottomNavigation from '../components/bottomNav/BottomNavigation.vue'
	import MyCircle from '../components/circle/Circle.vue'
	export default {
		components: {
			HealthHeader,
			TipInfo,
			BottomNavigation,
			MyCircle
		},
		data() {
			return {
				btnColor: '#dadada',
				deviceStatus: 0,
				data: [{
					value: 0,
					unit: 'CHOL',
				}, {
					value: 0,
					unit: 'HDL',
				}, {
					value: 0,
					unit: 'TRNG',
				}, {
					value: 0,
					unit: 'LDL',
				}], //数据
				blueDeviceList: [],
				deviceId: '', // 蓝牙设备的id
				serviceId: '', //设备的服务值
				characteristicId: '', // 设备的特征值
				userInfo: '',
				uid: 0, //用户选择的id
				username: '', //登录的名字
				// 底部工具栏
				page: '',
				toolList: [{
						img: require('@/static/icon/bloodPressure/month.png'),
						title: '月报',
						url: '/pages/healthMonitor/bloodFat/bloodFatMonth'
					},
					{
						img: require('@/static/icon/bloodPressure/device.png'),
						title: '设备',
						url: '/pages/mine/myDevice'
					},
					{
						img: require('@/static/icon/bloodPressure/write.png'),
						title: '手动录入',
						url: '/pages/healthMonitor/bloodFat/bloodFatManualEntry'
					},
				],
			};
		},
		onLoad(e) {
			this.userInfo = JSON.parse(uni.getStorageSync('userInfo'))
			this.uid = this.userInfo
			this.getUserInfo()
			this.initBlue()
			if (this.deviceId && this.deviceStatus === 0) {
				this.connect()

			}
		},
		//页面显示
		onShow() {
			uni.$on('backWithData', (data) => {
				this.uid = data.uid;
				this.username = data.name;
			});
		},
		methods: {
			getUserInfo() {
				this.$http.post('/user/info', {
					id: this.uid,
				}).then(res => {
					this.username = res.data.fullname
				})
			},
			handleMyUser() {
				uni.navigateTo({
					url: '/pages/homePage/myUsers?type=select' // 跳转到指定的目标页面
				});
			},
			handleDevelop() {

			},
			handleSaveHeat() {

				if (this.heat !== 0) {
					this.$refs.uToast.show({
						message: '保存成功',
						type: 'success',
					})
					this.btnColor = '#dadada'
					this.heat = 0
				}
			},
			// 初始化蓝牙
			initBlue() {
				uni.openBluetoothAdapter({
					success(res) {
						console.log('初始化蓝牙成功')
						console.log(res)
					},
					fail(err) {
						console.log('初始化蓝牙失败')
						console.error(err)
					}
				})
			},
			// 开始搜寻附近设备
			discovery() {
				const _this = this
				uni.startBluetoothDevicesDiscovery({
					success(res) {
						console.log('开始搜索')
						// 开启监听回调
						console.log(res)
						uni.onBluetoothDeviceFound(function(devices) {
							console.log(devices)
							_this.blueDeviceList.push(devices.devices[0])
						})
					},
					fail(err) {
						console.log('搜索失败')
						console.error(err)
					}
				})
			},
			// 【3】找到新设备就触发该方法
			found(res) {
				console.log(res)
				this.blueDeviceList.push(res.devices[0])

			},

			// 【4】连接设备
			connect(data) {
				const _this = this
				if (this.deviceId.length === 0) {
					this.deviceId = data.deviceId
				}

				uni.createBLEConnection({
					deviceId: this.deviceId,
					success(res) {
						console.log('连接成功')
						console.log(res)
						// 停止搜索

						setTimeout(() => {
							_this.notify()
						}, 1000)
						uni.showToast({
							title: '连接成功'
						})
					},
					fail(err) {
						console.log('连接失败')
						console.error(err)
						if (err.errCode === -1) {
							// 如果已经连接过则订阅通知
							_this.deviceStatus = 1
							_this.notify()
							return
						}
					}
				})
			},

			// 【5】停止搜索
			stopDiscovery() {
				uni.stopBluetoothDevicesDiscovery({
					success(res) {
						console.log('停止成功')
						console.log(res)
					},
					fail(err) {
						console.log('停止失败')
						console.error(err)
					}
				})
			},

			// 【6】获取服务
			getServices() {
				uni.getBLEDeviceServices({
					deviceId: this.deviceId,
					success(res) {
						console.log(res)
						uni.showToast({
							title: '获取服务成功'
						})
					},
					fail(err) {
						console.error(err)
						uni.showToast({
							title: '获取服务失败',
							icon: 'error'
						})
					}
				})
			},



			// 【7】获取特征值
			getCharacteristics() {
				uni.getBLEDeviceCharacteristics({
					deviceId: this.deviceId,
					serviceId: this.serviceId,
					success(res) {
						console.log(res)
						uni.showToast({
							title: '获取特征值成功'
						})
					},
					fail(err) {
						console.error(err)
						uni.showToast({
							title: '获取特征值失败',
							icon: 'error'
						})
					}
				})
			},


			// 【8】开启消息监听
			notify() {
				const _this = this
				uni.notifyBLECharacteristicValueChange({
					deviceId: this.deviceId,
					serviceId: this.serviceId,
					characteristicId: this.characteristicId,
					success(res) {
						console.log(res)
						_this.deviceStatus = 1
						_this.listenValueChange()

					},
					fail(err) {
						console.error(err)
						uni.showToast({
							title: '监听失败',
							icon: 'error'
						})
					}
				})
			},
			// ArrayBuffer转16进度字符串示例
			ab2hex(buffer) {
				const hexArr = Array.prototype.map.call(
					new Uint8Array(buffer),
					function(bit) {
						return ('00' + bit.toString(16)).slice(-2)
					}
				)

				return hexArr.join('')
			},
			// 【9】监听消息变化
			listenValueChange() {
				uni.onBLECharacteristicValueChange(res => {
					console.log(res)
					let resHex = this.ab2hex(res.value)
					this.processHeatData(res.value)
					console.log(resHex)
				})
			},
			// 处理温度
			processHeatData(buffer) {
				const data = new Int8Array(buffer);

				if (this.heat.length > 0 && this.heat.length < 8) {
					this.heat = new Int8Array([...this.heat, ...data]);
				} else if (data[0] === -81) {
					this.heat = data;
				}
				if (this.heat.length !== 8) return
				this.heat = (((this.heat[4] & 0xFF) << 8) + (this.heat[5] & 0xFF)) * 0.01;
				this.heat = Math.floor(parseFloat(this.heat) * 10) / 10;
				this.btnColor = '#01b09a'


			},
			onPageJump(url) {
				uni.navigateTo({
					url: url
				});

			},

		}
	}
</script>

<style lang="scss">
	.content {
		background-color: #fff;
		height: 100%;

		.data {
			.item {
				height: 250rpx;

				.value {

					font-size: 22px;
					font-weight: 400;
					color: #00b199;
				}

				.unit {
					font-size: 16px;
					color: #1aa58d;
				}
			}
		}
	}
</style>