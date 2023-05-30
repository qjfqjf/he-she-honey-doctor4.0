<template>
    <view class="d-flex flex-column bg-white">
        <z-nav-bar title="我的会员">

			<u-icon @click="goBack" class="ml-2" name="arrow-left" slot="left" color="#000000" size="24"></u-icon>

		</z-nav-bar>
        <u-search placeholder="请输入关键字" :show-action="false" shape="round" class="searchBar m-3" margin="20rpx" v-model="searchWords" height="40"
                  :clearabled="true"></u-search>
        <view class="d-flex a-center j-center buttonGrounp my-1 ">
            <u-button  :hairline="hairline"  color="rgb(31, 197, 162)" text="管理会员" class="leftButton" style="width: 250upx; margin-right: 30px ;"
                      ></u-button>
            <u-button  :hairline="hairline"  color="rgb(31, 197, 162)" text="我的会员" class="rightButton" style="width: 250upx;"
                      ></u-button>
        </view>
        <view>
            <u-index-list :index-list="indexList" active-color="#71d5a1">
                <template v-for="(item, index) in itemArr">
                    <!-- #ifdef APP-NVUE -->
                    <!--					<u-index-anchor :text="indexList[index]"></u-index-anchor>-->
                    <!-- #endif -->
                    <u-index-item>
                        <!-- #ifndef APP-NVUE -->
                        <u-index-anchor style="" :text="indexList[index]"></u-index-anchor>
                        <!-- #endif -->
                        <view class="list-cell" v-for="(cell, index) in item">
                            <view class="d-flex j-center a-center my-1">
                                <u--image  shape="circle" :showLoading="true" :src="avatar" width="40px" height="40px"></u--image>
                                <span class="list-cell">{{cell}}</span>
                            </view>
                        </view>
                    </u-index-item>
                </template>
            </u-index-list>
        </view>
    </view>
</template>

<script>
import IndexList from './indexList.vue'
export default {
    data() {
        return {
            searchWords: "",
            indexList: [ "W", "X", "Y", "Z", "#"]
            ,
            avatar: {"https://cdn.uviewui.com/uview/album/1.jpg",
			"https://cdn.uviewui.com/uview/album/2.jpg"}
            itemArr: [
                ['王树', '王建', '王坤'],
                ['肖雨涵', '肖子样'],
            ],
            hairline: false
        }
    },
    methods: {
        goBack(){
            uni.navigateBack({})
        },
    },
    components: {
        IndexList
    }
}
</script>

<style lang="scss" scoped>
.list-cell {
  display: flex;
  box-sizing: border-box;
  width: 100%;
  padding: 10px 24rpx;
  overflow: hidden;
  color: #323233;
  font-size: 14px;
  line-height: 24px;
  background-color: #fff;
}

.searchBar {

}

.buttonGrounp {

  .leftButton {
    border: 0;
    width: 40%;
    border-bottom-left-radius: 10px;
    border-top-left-radius: 10px;
  }

  .rightButton {
    border: 0;
    width: 40%;
    border-bottom-right-radius: 10px;
    border-top-right-radius: 10px;
  }
}
</style>
