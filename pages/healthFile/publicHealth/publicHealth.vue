<template>
	<view class="content">
		<!-- 顶nav-->
		<header-nav :title="title" :tourl="tourl" :addtext="addtext"></header-nav>
		<!-- 通用组件 -->
		<public-module></public-module>
		<!-- 数据列表为空 -->
		<view class="nothing" style="width: 400rpx" v-if="dataList.length === 0">
			<view>
				<empty-state :title="title" :tourl="tourl"></empty-state>
			</view>
		</view>
		<!-- 数据列表非空 -->
		<view class="something" v-else>

		</view>

	</view>
</template>

<script>
import emptyState from "../components/emptyState.vue";
import headerNav from "../components/headerNav.vue";
export default {
	components:{
		emptyState,
		headerNav
	},
	data() {
		return {
			//上面标题
			title:"基本公卫",
			//添加跳转页面路径
			tourl:"",
			addtext:"添加公卫",
			dataList:[]
		}
	},
	methods: {

	}
}
</script>

<style lang="scss">
.content{
	background-color: #FFFFFF;
	height: 100%;
	.nothing{
		text-align: center;
		margin: 0 auto;
	}
}
</style>
