<template>
	<view>
		<z-nav-bar title="执业信息" bgColor="#ffffff"></z-nav-bar>
		<!-- 公共组件-每个页面必须引入 -->
		<public-module></public-module>
		<view class="create">
			<u-cell-group :border="false" class="message" display="flex">
				<u-cell @click="showattrModal" titleStyle="font-size: 14px" size="large" icon="star-fill"
					:icon-style="iconStyle" title="执页属性" :isLink="true">
					<text slot="value" class="u-slot-value">{{ attrText }}</text>
				</u-cell>
				<u-cell @click="showpfdModal" titleStyle="font-size: 14px" size="large" icon="star-fill"
					:icon-style="iconStyle" title="擅长领域" :isLink="true">
					<text slot="value" class="u-slot-value">{{ pfdText }}</text>
				</u-cell>
				<u-cell @click="showdepaModal" class="message" titleStyle="font-size: 14px" size="large" icon="star-fill"
					:icon-style="iconStyle" title="科室" :value="birth" :isLink="true">
					<text slot="value" class="u-slot-value">{{ depaText }}</text>
				</u-cell>
				<u-cell @click="showjobModal" class="message" titleStyle="font-size: 14px" size="large" icon="star-fill"
					:icon-style="iconStyle" title="职称" :value="birth" :isLink="true">
					<text slot="value" class="u-slot-value">{{ jobText }}</text>
				</u-cell>
				<u-cell @click="" class="message" titleStyle="font-size: 14px" size="large" icon="star-fill"
					:icon-style="iconStyle" title="执业证书" :value="birth" :isLink="true">
					<text slot="value" class="u-slot-value"></text>
				</u-cell>
				<u-cell @click="" class="message" titleStyle="font-size: 14px" size="large" icon="star-fill"
					:icon-style="iconStyle" title="其他证书" :value="birth" :isLink="true">
					<text slot="value" class="u-slot-value"></text>
				</u-cell>
			</u-cell-group>
			<u-gap height="10"></u-gap>
			<u-cell-group :border="false" class="message">
				<u-cell size="large" icon="star-fill" :icon-style="iconStyle" title="选择省份" titleStyle="font-size: 14px"
					:isLink="true" @click="showarea = true">
					<text slot="value" class="u-slot-value">{{ areaText }}</text>
				</u-cell>
				<u-cell size="large" icon="star-fill" :icon-style="iconStyle" title="选择城市" titleStyle="font-size: 14px"
					:isLink="true" @click="showcity = true">
					<text slot="value" class="u-slot-value">{{ cityText }}</text>
				</u-cell>
				<u-cell size="large" icon="star-fill" :icon-style="iconStyle" title="选择区县" titleStyle="font-size: 14px"
					:isLink="true" @click="showvillage = true">
					<text slot="value" class="u-slot-value">{{ villageText }}</text>
				</u-cell>
				<u-cell size="large" icon="star-fill" :icon-style="iconStyle" title="机构类别" titleStyle="font-size: 14px"
					:isLink="true" @click="showorgan = true">
					<text slot="value" class="u-slot-value">{{ organText }}</text>
				</u-cell>
				<u-cell size="large" icon="star-fill" :icon-style="iconStyle" title="执业机构" titleStyle="font-size: 14px"
					:isLink="true" @click="showRelation = true">
					<text slot="value" class="u-slot-value">{{ organization }}</text>
				</u-cell>
			</u-cell-group>
			<view class="d-flex j-center">
				<u-button text="保存" size="large" type="success" shape="circle" color="rgb(10, 185, 156)"
					style="width: 660rpx; height: 110rpx" @click="saveDoctor()"></u-button>
			</view>
		</view>
		<u-modal title="机构" :show="showRelation" showCancelButton closeOnClickOverlay confirmColor="rgb(10, 185, 156)"
			@confirm="confirm9($event)" @cancel="() => (showRelation = false)" @close="() => (showRelation = false)">
			<u--input placeholder="请输入机构名" border="surround" v-model="organization"></u--input>
		</u-modal>
		<u-picker :columns="attr" :show="showattr" close-on-click-overlay @cancel="cancel0" @close="close0"
			@confirm="confirm0($event)">
			<template #cancel>
				<div>取消</div>
			</template>
			<template #confirm>
				<div>确定</div>
			</template>
		</u-picker>
		<u-picker :columns="pfd" :show="showpfd" close-on-click-overlay @cancel="cancel1" @close="close1"
			@confirm="confirm1($event)">
			<template #cancel>
				<div>取消</div>
			</template>
			<template #confirm>
				<div>确定</div>
			</template>
		</u-picker>
		<u-picker :columns="depa" :show="showdepa" close-on-click-overlay @cancel="cancel2" @close="close2"
			@confirm="confirm2($event)">
			<template #cancel>
				<div>取消</div>
			</template>
			<template #confirm>
				<div>确定</div>
			</template>
		</u-picker>
		<u-picker :columns="job" :show="showjob" close-on-click-overlay @cancel="cancel3" @close="close3"
			@confirm="confirm3($event)">
			<template #cancel>
				<div>取消</div>
			</template>
			<template #confirm>
				<div>确定</div>
			</template>
		</u-picker>

		<u-picker :columns="area" :show="showarea" close-on-click-overlay @cancel="cancel5" @close="close5"
			@confirm="confirm5($event)">
			<template #cancel>
				<div>取消</div>
			</template>

			<template #confirm>
				<div>确定</div>
			</template>
		</u-picker>
		<u-picker :columns="city" :show="showcity" close-on-click-overlay @cancel="cancel6" @close="close6"
			@confirm="confirm6($event)">
			<template #cancel>
				<div>取消</div>
			</template>
			<template #confirm>
				<div>确定</div>
			</template>
		</u-picker>
		<u-picker :columns="village" :show="showvillage" close-on-click-overlay @cancel="cancel7" @close="close7"
			@confirm="confirm7($event)">
			<template #cancel>
				<div>取消</div>
			</template>
			<template #confirm>
				<div>确定</div>
			</template>
		</u-picker>
		<u-picker :columns="organ" :show="showorgan" close-on-click-overlay @cancel="cancel8" @close="close8"
			@confirm="confirm8($event)">
			<template #cancel>
				<div>取消</div>
			</template>
			<template #confirm>
				<div>确定</div>
			</template>
		</u-picker>
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
			attr: [[]],
			pfd: [[]],
			depa: [[]],
			job: [[]],
			organ: [[]],
			area: [[]],
			city: [[]],
			village: [[]],
			attrList: [],
			pfdList: [],
			depaList: [],
			jobList: [],
			organList: [],
			areaList: [],
			cityList: [],
			villageList: [],
			userInfo: {
				name: '',
			},
			showInfo: {

			},
			// nameValue: '',
			// idCardNumberValue: '',
			// telValue: '',
			// codeValue: '',
			// heightValue: '',
			// weightValue: '',
			// relationShip: '',
			// gender: '',
			// relationShipText: '',
			// chooseDate: Number(new Date()),

			attrText: '',
			pfdText: '',
			depaText: '',
			jobText: '',
			areaText: '',
			cityText: '',
			villageText: '',
			organText: '',
			organization: '',
			area_id: '',
			city_id: '',
			village_id: '',
			showattr: false,
			showpfd: false,
			showdepa: false,
			showjob: false,
			showorgan: false,
			showarea: false,
			showcity: false,
			showvillage: false,
			showorgan: false,
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
	onLoad: function (opt) {
		console.log(opt.e);
		this.selectUser()
		this.getDoctor()
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
		getDoctor() {
			this.$http.get("/practice/index", {
				uid: uni.getStorageSync('userInfo')
			}).then((res) => {
				console.log(res);
				this.attrText = res.data.attr_cn;
				this.pfdText = res.data.pfd_cn;
				this.depaText = res.data.depa_cn;
				this.jobText = res.data.job_cn;
				this.areaText = res.data.province_cn;
				this.cityText = res.data.city_cn;
				this.villageText = res.data.district_cn
				this.organText = res.data.organ_cn
				this.organization = res.data.organization;
			})
		},
		selectUser() {
			this.$http.get("/practice/getConfig", {}).then((res) => {
				console.log(res);
				for (let i = 0; i < res.data.attr.length; i++) {
					this.attr[0].splice(i, 1, res.data.attr[i].name);
					this.attrList.splice(i, 1, res.data.attr[i]);
				}
				for (let i = 0; i < res.data.pfd.length; i++) {
					this.pfd[0].splice(i, 1, res.data.pfd[i].name);
					this.pfdList.splice(i, 1, res.data.pfd[i]);
				}
				for (let i = 0; i < res.data.depa.length; i++) {
					this.depa[0].splice(i, 1, res.data.depa[i].name);
					this.depaList.splice(i, 1, res.data.depa[i]);
				}
				for (let i = 0; i < res.data.job.length; i++) {
					this.job[0].splice(i, 1, res.data.job[i].name);
					this.jobList.splice(i, 1, res.data.job[i]);
				}
				for (let i = 0; i < res.data.organ.length; i++) {
					this.organ[0].splice(i, 1, res.data.organ[i].name);
					this.organList.splice(i, 1, res.data.organ[i]);
				}
				for (let i = 0; i < res.data.area.length; i++) {
					this.area[0].splice(i, 1, res.data.area[i].name);
					this.areaList.splice(i, 1, res.data.area[i]);
					if (res.data.area[i].data) {
						for (let j = 0; j < res.data.area[i].data.length; j++) {
							this.cityList.push(res.data.area[i].data[j]);
							if (res.data.area[i].data[j].data) {
								for (let x = 0; x < res.data.area[i].data[j].data.length; x++) this.villageList.push(res.data.area[i].data[j].data[x]);
							}
						}

					}

				}

				console.log('attr', this.attr);
				console.log('pfd', this.pfd);
				console.log('depa', this.depa);
				console.log('job', this.job);
				console.log('organ', this.organ);
				// console.log('area',this.area);
				// console.log('city',this.cityList);
				console.log('village', this.villageList);
			})
		},
		saveDoctor() {
			let save = {}
			if (this.attrText) {
				const attr = this.attrList.find(obj => obj.name === this.attrText);
				save.attr_id = attr.id;
			}
			if (this.jobText) {
				const job = this.jobList.find(obj => obj.name === this.jobText);
				save.job_id = job.id;
			}
			if (this.pfdText) {
				const pfd = this.pfdList.find(obj => obj.name === this.pfdText);
				save.pfd_id = pfd.id;
				save.pfd_cn = this.pfdText
			}
			if (this.depaText) {
				const depa = this.depaList.find(obj => obj.name === this.depaText);
				save.depa_id = depa.id;
				save.depa_text = this.depaText;
			}
			if (this.organText) {
				const organ = this.organList.find(obj => obj.name === this.organText);
				save.organ_id = organ.id;
				save.organization = this.organization
			}
			// if(this.organText){
			// 	const organ = this.organList.find(obj => obj.name === this.organText);
			// 	save.organ_id = organ.id;
			// 	save.organization = this.organization
			// }
			save.province_id = this.area_id
			save.city_id = this.city_id
			save.district_id = this.village_id
			console.log('save', save);
			this.$http.post('/practice/save', {
				...save
			}).then((res) => {
				console.log('res', res);
				if (res.code == 20000) {
					uni.showToast({
						title: '保存成功',
						icon: 'none',
						duration: 2000,
					})
					setTimeout(() => {
						uni.navigateBack({
							delta: 1,
						})
					}, 1000)
				} else {
					uni.showToast({
						title: '保存失败',
						icon: 'none',
						duration: 2000,
					})
					setTimeout(() => {
						uni.navigateBack({
							delta: 1,
						})
					}, 1000)
				}
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
			this.showpfd = false
		},
		cancel1() {
			this.showpfd = false
		},
		close2() {
			this.showdepa = false
		},
		cancel2() {
			this.showdepa = false
		},
		close3() {
			this.showjob = false
		},
		cancel3() {
			this.showjob = false
		},
		close4() {
			this.showpfd = false
		},
		cancel4() {
			this.showpfd = false
		},
		close5() {
			this.showarea = false
		},
		cancel5() {
			this.showarea = false
		},
		close6() {
			this.showcity = false
		},
		cancel6() {
			this.showcity = false
		},
		close7() {
			this.showvillage = false
		},
		cancel7() {
			this.showvillage = false
		},
		close8() {
			this.showorgan = false
		},
		cancel8() {
			this.showorgan = false
		},
		confirm0(e) {
			this.attrText = e.value.toString();
			this.showattr = false;
		},
		confirm1(e) {
			this.pfdText = e.value.toString();
			this.showpfd = false;
		},
		confirm2(e) {
			this.depaText = e.value.toString();
			this.showdepa = false;
		},
		confirm3(e) {
			this.jobText = e.value.toString();
			this.showjob = false;
		},
		confirm5(e) {
			console.log('e', e)
			this.areaText = e.value.toString();
			const area = this.areaList.find(obj => obj.name === this.areaText);
			console.log('area', area);
			this.area_id = area.id
			const cityList = this.cityList.filter(obj => obj.parent_id === area.id);
			console.log('city', cityList)
			for (let i = 0; i < cityList.length; i++) {
				this.city[0].splice(i, 1, cityList[i].name);
			}
			console.log('city', this.city[0]);
			this.showarea = false;
		},
		confirm6(e) {
			console.log('e', e)
			this.cityText = e.value.toString();
			const city = this.cityList.find(obj => obj.name === this.cityText);
			console.log('city', city);
			this.city_id = city.id
			const villageList = this.villageList.filter(obj => obj.parent_id === city.id);
			console.log('village', villageList)
			for (let i = 0; i < villageList.length; i++) {
				this.village[0].splice(i, 1, villageList[i].name);
			}
			console.log('village[0]', this.village[0]);
			this.showcity = false;
		},
		confirm7(e) {
			console.log('e', e)
			this.villageText = e.value.toString();
			const village = this.villageList.find(obj => obj.name === this.villageText);
			this.village_id = village.id
			this.showvillage = false;
		},
		confirm8(e) {
			console.log('e', e)
			this.organText = e.value.toString();
			this.showorgan = false;
		},
		confirm9(e) {
			this.showRelation = false;
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
	onHide() { },
	//页面卸载
	onUnload() { },
	//页面下来刷新
	onPullDownRefresh() { },
	//页面上拉触底
	onReachBottom() { },
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