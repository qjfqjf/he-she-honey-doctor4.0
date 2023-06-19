<template>
	<view class="container h-100 w-100 flex-column d-flex">
		<public-module></public-module>
		<z-nav-bar home title="数字健康管理" class="HomeNavBar" bg-color="#bef1d0" fontColor="black">
			<img slot="left" :src="homePageIcons.Scanning.icon" class="small-icon p-2" alt=""></img>
			<img slot="right" :src="homePageIcons.Location.icon" class="small-icon p-2" alt=""></img>
		</z-nav-bar>
		
		<view class="top-bar d-flex j-sb w-100 a-center my-2 h-100">
			<u-button class="leftRoundButton border" color="#18b566" @click="changeStatu">{{workStatu}}
			</u-button>
			<view class="Avatar">
				<u-avatar :src="avatar" size="40"></u-avatar>
				<view style="font-size: 26upx; font-weight: bold;">{{ name }}</view>
			</view>
			<u-button class="rightRoundButton h-100 border" @click="navto" color="#18b566">我的会员
			</u-button> 
		</view>

		<view class="swiper">
			<view class="w-100 rounded-20 " style="background-color: white">
				<swiper :indicator-dots="true" class="swiper">
					<swiper-item v-for="(page,index) in appFeature" :key="index">
						<view class="d-flex">
							<view class="d-flex f-grow-1 flex-column a-center j-center p-1" v-for="(item,index) in page"
								:key="index">
								<view><img :src="item.icon" class="big-icon" alt=""></view>
								<view>
									{{ item.name }}
								</view>
							</view>
						</view>
					</swiper-item>
				</swiper>
			</view>
		</view>
		<!-- <u-swiper class="swiper mx-1" :list="wisperImage" previousMargin="30" nextMargin="30" circular :autoplay="false"
			radius="5" bgColor="#ffffff"></u-swiper> -->
		<u-swiper class=" m-1" :list="wisperImage" indicator indicatorMode="line" circular
			radius="5" bgColor="#ffffff">
		</u-swiper>
		<view class="m-1 rounded-20 bg-white"> 

			<u-gap height="10"></u-gap> 
			<view class="m-1 rounded-20 bg-white">
				<u-grid :border="false" col="4">
					<u-grid-item v-for="(listItem,listIndex) in appManage" :key="listIndex" @click="dev(listIndex)">
						<navigator :url="listItem.path" class="nav">
							<u--image class="appManeger_block_icon" :src="listItem.icon"  height="90upx" width="90upx">
							</u--image>
							<u--text :text="listItem.name" align="center"></u--text>
						</navigator>
					</u-grid-item>
				</u-grid>
				<u-toast ref="uToast" />
			</view>
			<z-navigation></z-navigation>
		</view>


	</view>
</template>

<script>
	import {
		wisperImage,
		appManage,
		appFeature,
		homePageIcons
	} from "../../static/js/homePage/staticData";
	import UImage from "../../uni_modules/uview-ui/components/u--image/u--image.vue";
	import home from "../template/home.vue";
	import UButton from "../../uni_modules/uview-ui/components/u-button/u-button.vue";
	// import SwiperList from "../../scrollAvatar/components/swiper-list/swiper-list.vue";
	export default {
		computed: {
			home() {
				return home
			}
		}, 
		data() {
			return {
				workStatu:'关闭值班',
				token: uni.getStorageSync('access-token'),
				wisperImage,
				appManage, 
				appFeature,
				homePageIcons,
				avatar: 'https://cdn.uviewui.com/uview/album/1.jpg',
				name: '平台管理员',
			};
		},
		components: {
			UButton,
			UImage,
			// SwiperList
		},
		//第一次加载
		onLoad(e) {
			// 隐藏原生的tabbar
			uni.hideTabBar();

			if (!this.token) {
				uni.navigateTo({
					url: '/pages/login/login',
				})
			}
		},
		//页面显示
		onShow() {
			// 隐藏原生的tabbar
			uni.hideTabBar();
		},
		//方法
		methods: {
			changeStatu(){
				if(this.workStatu == '关闭值班'){
					this.workStatu = '开启值班'
				}else{
					this.workStatu = '关闭值班'
				}
			},
			//开发中...
			dev(listIndex){
				if(listIndex == 3 || listIndex >= 6){
					uni.showToast({
						title:"开发中...",
						icon:"none"
					})
				}
			},
			switchChange() {

			},
			navto() {
				uni.navigateTo({
					url: "/pages/homePage/myMembers"
				});
			},
			onPageJump(url) {
				uni.navigateTo({
					url: url
				});
				console.log(111)
			},
			onTokenJump(url) {
				this.judgeLogin(() => {
					uni.navigateTo({
						url: url
					});
				});
			},
			onPrivacyAgreement() {
				// #ifdef H5
				window.open("https://ask.dcloud.net.cn/article/36937");
				// #endif
				// #ifndef H5
				this.$store.commit("setWebViewUrl", "https://ask.dcloud.net.cn/article/36937");
				uni.navigateTo({
					url: '/pages/template/webView'
				});
				// #endif
			},
			changeHeadImg(index) {
				console.log('当前选中' + index)
			}

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
			return this.wxShare();
		}
	};
</script>
<style lang="scss" scoped>
	.HomeNavBar {
		background-color: rgba(255, 255, 255, 0);
	}

	.small-icon {
		height: 40upx;
		width: 40upx;
	}

	.medium-icon {
		height: 60upx;
		width: 60upx;
	}

	.big-icon {
		height: 120upx;
		width: 120upx;
	}

	.statusBar {
		border-radius: 30%;
		background-color: white; 

	}

	.leftRoundButton {
		height: 100upx;
		width: 180upx;
		border-bottom-right-radius: 50px;
		border-top-right-radius: 50px;
		font-size: 15px;
	}

	.rightRoundButton {
		height: 100upx;
		width: 180upx;
		border-bottom-left-radius: 50px;
		border-top-left-radius: 50px;
		font-size: 15px;
	}

	.roundButton {
		height: 80upx;
		width: 80upx;
	}

	.Avatar {
		width: 50%;
		height: 80upx;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}

	.nav{
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}
	.appFeature {
		border-radius: 50px;
		padding: 10px;

		&_Row {
			margin-top: 1px;
			margin-bottom: 1px;
		}

		.appFeatureBLock {
			border: 2px white;
			height: 120upx;
			border-radius: 5px;

		}
	}

	.container {
		background-color: #bef1d0;
	}

	.swiper {
		border-radius: 5px;
		height: 260rpx !important;
	}

	.appManeger {
		&_block {
			height: 180upx;
			
			&_icon {
				padding-top: 20rpx;
				padding-bottom: 15upx;
			}

			&_name {}
		}
	}

	.swiper {
		height: 150px;
	}

	.unit {
		font-size: 12upx;
	}
</style>
