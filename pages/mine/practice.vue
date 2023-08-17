<template>
	<view>
		<z-nav-bar title="执业信息" bgColor="#ffffff"></z-nav-bar>
		<!-- 公共组件-每个页面必须引入 -->
		<public-module></public-module>
		<view class="create">
			<u-cell-group :border="false" class="message" display="flex">
				<u-cell @click="showattrModal" titleStyle="font-size: 14px" size="large" icon="star-fill"
					:icon-style="iconStyle" title="执页属性" :isLink="true">
					<text slot="value" class="u-slot-value"></text>
				</u-cell>
				<!-- <u-cell @click="showpfdModal" titleStyle="font-size: 14px" size="large" icon="star-fill"
					:icon-style="iconStyle" title="擅长领域" :isLink="true">
					<text slot="value" class="u-slot-value"></text>
				</u-cell>
				<u-cell @click="showdepaModal" class="message" titleStyle="font-size: 14px" size="large"
					icon="star-fill" :icon-style="iconStyle" title="科室" :value="birth" :isLink="true">
					<text slot="value" class="u-slot-value"></text>
				</u-cell>
				<u-cell @click="showjobModal" class="message" titleStyle="font-size: 14px" size="large" icon="star-fill"
					:icon-style="iconStyle" title="职称" :value="birth" :isLink="true">
					<text slot="value" class="u-slot-value"></text>
				</u-cell>
				<u-cell @click="" class="message" titleStyle="font-size: 14px" size="large" icon="star-fill"
					:icon-style="iconStyle" title="执业证书" :value="birth" :isLink="true">
					<text slot="value" class="u-slot-value"></text>
				</u-cell>
				<u-cell @click="" class="message" titleStyle="font-size: 14px" size="large" icon="star-fill"
					:icon-style="iconStyle" title="其他证书" :value="birth" :isLink="true">
					<text slot="value" class="u-slot-value"></text>
				</u-cell> -->
			</u-cell-group>
			<u-gap height="10"></u-gap>
			<!-- <u-cell-group :border="false" class="message">
				<u-cell size="large" icon="star-fill" :icon-style="iconStyle" title="选择省份" titleStyle="font-size: 14px"
					:isLink="true" @click="showareaModal = true">
					<text slot="value" class="u-slot-value"></text>
				</u-cell>
				<u-cell size="large" icon="star-fill" :icon-style="iconStyle" title="选择城市" titleStyle="font-size: 14px"
					:isLink="true" @click="showareaModal = true">
					<text slot="value" class="u-slot-value"></text>
				</u-cell>
				<u-cell size="large" icon="star-fill" :icon-style="iconStyle" title="选择区县" titleStyle="font-size: 14px"
					:isLink="true" @click="showareaModal = true">
					<text slot="value" class="u-slot-value"></text>
				</u-cell>
				<u-cell size="large" icon="star-fill" :icon-style="iconStyle" title="机构类别" titleStyle="font-size: 14px"
					:isLink="true" @click="showRelation = true">
					<text slot="value" class="u-slot-value"></text>
				</u-cell>
				<u-cell size="large" icon="star-fill" :icon-style="iconStyle" title="执业机构" titleStyle="font-size: 14px"
					:isLink="true" @click="showRelation = true">
					<text slot="value" class="u-slot-value"></text>
				</u-cell>
			</u-cell-group> -->
		</view>
		<u-picker mode="selector" :columns="attr" :show="showattr" close-on-click-overlay @cancel="cancel0"
			@close="close0" @confirm="confirm0">
		</u-picker>
		<!-- <picker :value="attrText" :range="attr" range-key="name"></picker>> -->
		<u-picker :columns="pfd" :show="showpfd" close-on-click-overlay @cancel="cancel0" @close="close0"
			@confirm="confirm0">
			<template #cancel>
				<div>取消</div>
			</template>
			<template #confirm>
				<div>确定</div>
			</template>
		</u-picker>
		<u-picker :columns="area" :show="showarea" close-on-click-overlay @cancel="cancel0" @close="close0"
			@confirm="confirm0"></u-picker>
	</view>
</template>

<script>
	import UPicker from "../../uni_modules/uview-ui/components/u-picker/u-picker.vue";
	export default {
		components: {
			UPicker
		},
		data() {
			return {
				images: 'https://img2.baidu.com/it/u=1834432083,2460596852&fm=253&fmt=auto&app=138&f=JPEG?w=500&h=500',
				iconStyle: {
					"font-size": '10px',
					"color": 'red'
				},
				attr: [],
				pfd: [
					[]
				],
				depa: [
					[],
					[]
				],
				job: [
					[],
					[]
				],
				organ: [
					[],
					[]
				],
				area: [
					[],
					[]
				],
				userInfo: {
					name: '',
				},
				showInfo: {

				},
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

				attrText: '',
				showattr: false,
				showpfd: false,
				showdepa: false,
				showjob: false,
				showorgan: false,
				showarea: false,
				showHeight: false,
				showWeight: false,
				showRelation: false,
				popupOptions: {
					placeholder: '',
				},
				actions: [{
						name: '男',
						value: '0',
					},
					{
						name: '女',
						value: '1',
					},
				],
				actionsRelation: [{
						name: '本人',
						value: 'myself',
					},
					{
						name: '父亲',
						value: 'father',
					},
					{
						name: '母亲',
						value: 'mother',
					},
					{
						name: '兄弟姐妹',
						value: 'broAndSis',
					},
					{
						name: '子女',
						value: 'child',
					},
					{
						name: '其他',
						value: 'other_relatives',
					},
				],
				rules: {
					'userInfo.sex': {
						type: 'string',
						max: 1,
						required: true,
						message: '请选择男或女',
						trigger: ['blur', 'change'],
					},
				},
				avatar: 'https://cdn.uviewui.com/uview/album/3.jpg',
				genderText: '请选择您的性别',
				name: '请输入您的真实姓名',
				phone: '请输入您的电话号码',
				code: '请输入您的验证码',
				birth: '请选择您的出生日期',
				idCardNumber: '请输入您的身份证号',
				tel: '请输入您的电话号码',
				height: '请输入您的身高',
				weight: '请输入您的体重',
				type: '',
				genderValue: 0,
				relationValue: 0,
				codeMsg: '',
			}
		},
		onLoad: function(opt) {
			console.log(opt.e);
			this.selectUser()
			// console.log(111)
			// _this = this;
			// console.log('type', opt.type);
			// this.type = opt.type
			//判断是否为添加页面，如果不是，则查询当前用户数据并回显
			// console.log('id0',uni.getStorageSync('userInfo'));
			// if (this.type != 'add') {
			// 	if(opt.e){
			// 		uni.setStorageSync('userInfo', opt.e)
			// 		console.log('id',uni.getStorageSync('userInfo'));
			// 	}

			// }
		},
		methods: {
			selectUser() {
				this.$http.post("/practice/getConfig", {}).then((res) => {
					console.log(res);
					this.attr = res.data.attr;
					// for (let i = 0; i < res.data.pfd.length; i++) this.pfd[0][i] = res.data.pfd[i].name;
					// for (let i = 0; i < res.data.depa.length; i++) this.depa[i] = res.data.depa[i].name;
					// for (let i = 0; i < res.data.job.length; i++) this.job[i] = res.data.job[i].name;
					// for (let i = 0; i < res.data.organ.length; i++) this.organ[i] = res.data.organ[i].name;
					// for (let i = 0; i < res.data.attr.length; i++) {
					// 	this.attr.push(`attr[${i}]`);
					// }
					// console.log('pfd', this.pfd);
					// console.log('depa', this.depa);
					// console.log('job', this.job);
					// console.log('organ', this.organ);
					// console.log('area', this.area);
					this.$forceUpdate();

				})
			},
			btn0() {
				this.show0 = true
			},
			btn1() {
				this.show2 = true
			},
			close0() {
				this.showattr = false
			},
			cancel0() {
				this.showattr = false
			},
			close1() {
				this.show2 = false
			},
			cancel1() {
				this.show2 = false
			},
			confirm0(e) {
				this.show1 = true
				this.show0 = false;
			},
			confirm1(e) {
				this.department = e.value[0]
				this.show3 = true
				this.show2 = false;
			},
			showattrModal() {
				console.log(this.attr);
				this.showattr = true
			},
			showpfdModal() {
				this.showpfd = true
			},
			showdepaModal() {
				this.showdepa = true
			},
			showjobModal() {
				this.showjob = true
			},
			showorganModal() {
				this.showorgan = true
			},
			showareaModal() {
				this.showarea = true
			},
			confirmName() {
				const reg = /^[\u4E00-\u9FA5]{2,5}$/
				if (!reg.test(this.nameValue)) {
					// 如果名字长度不符合要求，则给出提示
					uni.showToast({
						title: '姓名格式不对',
						icon: 'none',
					})
					return
				}
				this.name = this.nameValue
				this.userInfo.fullname = this.nameValue
				this.showName = false
			},
			confirmBirth() {
				const timestamp = this.chooseDate
				const date = new Date(timestamp)
				const year = date.getFullYear()
				const month = String(date.getMonth() + 1).padStart(2, '0') // 注意月份从 0 开始计数，需要加 1，并且需要补齐位数
				const day = String(date.getDate()).padStart(2, '0') // 注意日期需要补齐位数
				this.birth = `${year}-${month}-${day}`
				this.userInfo.birthday = this.birth
				this.showBirth = false
			},
			genderSelect(e) {
				this.gender = e.value
				this.genderText = e.name
			},
			confirmIdCardNumber() {
				console.log(this.idCardNumberValue, 11111)
				const reg = /(^\d{15}$)|(^\d{18}$)|(^\d{17}(\d|X|x)$)/
				if (!reg.test(this.idCardNumberValue)) {
					uni.showToast({
						title: '请输入正确的身份证号',
						icon: 'none',
					})
					return
				}
				// 校验身份证号码的前两位是否为有效的省份代码
				var provinceCode = this.idCardNumberValue.substring(0, 2)
				if (!this.isValidProvinceCode(provinceCode)) {
					uni.showToast({
						title: '请输入正确的身份证号',
						icon: 'none',
					})
					return
				}
				// 校验身份证号码出生日期是否合法
				var birthday = this.getBirthdayFromIdCardNumber(this.idCardNumberValue)
				if (!this.isValidBirthday(birthday)) {
					uni.showToast({
						title: '请输入正确的身份证号',
						icon: 'none',
					})
					return
				}
				this.idCardNumber = this.idCardNumberValue
				this.userInfo.id_card = this.idCardNumberValue
				this.showIdCardNumber = false
			},
			confirmTel() {
				const reg = /^1[3-9]\d{9}$/
				if (!reg.test(this.telValue)) {
					// 如果名字长度不符合要求，则给出提示
					uni.showToast({
						title: '请输入正确的手机号',
						icon: 'none',
					})
					return
				}
				this.tel = this.telValue
				this.userInfo.phone_number = this.tel
				this.showTel = false
			},
			confirmCode() {

				this.code = this.codeValue
				this.userInfo.code = this.code
				this.showCode = false
			},
			confirmHeight() {
				// 将输入转为数值
				const inputHeightNum = Number(this.heightValue)
				// 判断是否为空
				if (this.inputHeight === '') {
					uni.showToast({
						title: '请输入身高',
						icon: 'none',
					})
					return
				}
				// 判断是否为数字
				if (isNaN(inputHeightNum)) {
					uni.showToast({
						title: '身高必须为数字',
						icon: 'none',
					})
					return
				}
				// 判断范围是否合法
				if (inputHeightNum < 50 || inputHeightNum > 250) {
					uni.showToast({
						title: '请输入50-250之间的数字',
						icon: 'none',
					})
					return
				}
				this.height = this.heightValue
				this.userInfo.stature = this.height
				console.log('stature', this.userInfo.stature);
				this.showHeight = false
			},
			confirmWeight() {
				// 将输入转为数值
				const inputWeightNum = Number(this.weightValue)
				// 判断是否为数字
				if (isNaN(inputWeightNum)) {
					uni.showToast({
						title: '身高必须为数字',
						icon: 'none',
					})
					return
				}
				this.weight = this.weightValue
				this.userInfo.weight = this.weight
				this.showWeight = false
			},
			// 校验身份证号码的前两位是否为有效的省份代码
			isValidProvinceCode(provinceCode) {
				var provinces = [
					'11',
					'12',
					'13',
					'14',
					'15',
					'21',
					'22',
					'23',
					'31',
					'32',
					'33',
					'34',
					'35',
					'36',
					'37',
					'41',
					'42',
					'43',
					'44',
					'45',
					'46',
					'50',
					'51',
					'52',
					'53',
					'54',
					'61',
					'62',
					'63',
					'64',
					'65',
					'71',
					'81',
					'82',
				]
				return provinces.indexOf(provinceCode) !== -1
			},
			// 校验身份证号码出生日期是否合法
			isValidBirthday(birthday) {
				return birthday !== null && birthday <= new Date()
			},

			// 根据身份证号码获取出生日期
			getBirthdayFromIdCardNumber(idCardNumber) {
				var birthday = null
				if (idCardNumber.length === 15) {
					birthday = new Date(
						idCardNumber.substring(6, 8),
						idCardNumber.substring(8, 10) - 1,
						idCardNumber.substring(10, 12)
					)
				} else if (idCardNumber.length === 18) {
					birthday = new Date(
						idCardNumber.substring(6, 10),
						idCardNumber.substring(10, 12) - 1,
						idCardNumber.substring(12, 14)
					)
				}
				return birthday
			},
			onSubmit() {
				if (this.avatar == '') {
					uni.showToast({
						title: '请上传头像',
						icon: 'none',
					})
					return
				}
				if (this.nickname == '') {
					uni.showToast({
						title: '请输入昵称',
						icon: 'none',
					})
					return
				}
				let httpData = {
					nickname: this.nickname,
					avatar: this.avatar,
				}
				if (this.phone) {
					if (!this.$base.phoneRegular.test(this.phone)) {
						uni.showToast({
							title: '请输入正确的手机号',
							icon: 'none',
						})
						return
					}
					if (this.phone != this.userInfo.phone) {
						httpData.phone = this.phone
					}
				}
				// this.$http.post('api/common/v1/edit_user_info', httpData).then((res) => {
				// 	this.setuserInfo({
				// 		nickname: this.nickname,
				// 		avatar: this.avatar,
				// 		phone: this.phone || this.userInfo.phone,
				// 	})
				// 	uni.showToast({
				// 		title: '修改成功！',
				// 	})
				// })
			},
		},
		//页面隐藏
		onHide() {},
		//页面卸载
		onUnload() {},
		//页面下来刷新
		onPullDownRefresh() {},
		//页面上拉触底
		onReachBottom() {},
		//用户点击分享
		onShareAppMessage(e) {
			return this.wxShare()
		},
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