<template>
	<view>
		<z-nav-bar backState="2000" title="我的"></z-nav-bar>
		<u-gap
			height="10"
			bgColor="#fff"
		></u-gap>
		<!-- 公共组件-每个页面必须引入 -->
		<public-module></public-module>  
		<u-cell-group>
			<u-cell size="large" class="message" icon="../../static/icon/integral/my.png" url="/pages/mine/editInfo" title="我的资料"></u-cell>
			<u-cell size="large" class="message" icon="../../static/icon/integral/execution.png" url="/pages/mine/practice" title="执业信息(必填)"></u-cell>
			<u-cell size="large" class="message" icon="../../static/icon/integral/personalProfile.png" url="" title="个人简介"></u-cell>
		</u-cell-group>
		<u-gap
			height="10"
		></u-gap>
		<u-cell-group> 
			<u-cell size="large" class="message" icon="../../static/icon/integral/mydevice.png" url="/pages/mine/myDevice" title="我的设备"></u-cell>
			<u-cell size="large" class="message" icon="../../static/icon/integral/myservice.png" url="" title="我的服务"></u-cell>
			<u-cell size="large" class="message" icon="../../static/icon/integral/exchange.png" url="/pages/mine/myComment" title="我的评价"></u-cell>	
		</u-cell-group>
		<u-gap
			height="10" 
		></u-gap>
		<u-cell-group>
			<u-cell size="large" class="message" icon="../../static/icon/integral/setting.png" url="/pages/mine/setting" title="设置"></u-cell>
			<u-cell size="large" class="message" icon="../../static/icon/integral/help.png" url="/pages/mine/help" title="帮助"></u-cell>
		</u-cell-group>	
		<u-gap
			height="50"
		></u-gap>
		<view class="but">
			<u-button
				@click="exit"
				text="退出"
				size="normal"
				type="error"
				shape="circle"
				style="height: 100rpx; width:660rpx"
			></u-button>
		</view>
		<u-modal
			title="温馨提示"
			:show="showExit"
			showCancelButton
			confirmColor="rgb(10, 185, 156)"
			@confirm="confirmExit"
			@cancel="() => showExit = false"
		><text>你确定要退出登录吗？</text>
		</u-modal>
		<z-navigation></z-navigation>
	</view>
</template>

<script>
export default {
	data() {
		return {
			showExit: false,
		};
	},
	//第一次加载
	onLoad(e) {
		// 隐藏原生的tabbar
		uni.hideTabBar();
	},
	//页面显示
	onShow() {
		// 隐藏原生的tabbar
		uni.hideTabBar();
	},
	//方法
	methods: {
		exit() {
			this.showExit = true;
			console.log("1111111111111");
		},
		confirmExit() {
			this.showExit = false
			// 清除所有的缓存
			uni.clearStorageSync()
			// 跳转到登录页面
			uni.reLaunch({
				url: '/pages/login/login',
			})
		},
		onPageJump(url) {
			uni.navigateTo({
				url: url
			});
		},
		onTokenJump(url) {
			this.judgeLogin(() => {
				// 这里写登录后的代码，未登录不会到这里来，会自动提示去登录
				uni.navigateTo({
					url: url
				});
			});
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
@import '@/style/mixin.scss';
.message{
	background-color: #fff;
}
.but {
	display: flex; 
	justify-content: center;
}
</style>
