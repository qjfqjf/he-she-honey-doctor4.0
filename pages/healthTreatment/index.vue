<template>
  <view class="content p-2">
    <z-nav-bar title="诊疗/调理"></z-nav-bar>
    <public-module></public-module>
    <view class="title">
      <text>诊疗/调理</text>
    </view>
    <!-- 设备板块 -->
    <view class="devices-warp mt-2">
      <u-grid :border="false" col="4">
        <u-grid-item class="item" v-for="(baseListItem,baseListIndex) in baseList" :key="baseListIndex"
          @click="click(baseListItem.url,baseListItem.title)">
          <image style="width: 80rpx;height: 80rpx;" :src="baseListItem.img" mode="aspectFit"></image>
          <text class="grid-text mt-2">{{baseListItem.title}}</text>
        </u-grid-item>
      </u-grid>
    </view>
    <u-toast ref="uToast"></u-toast>
  </view>
</template>

<script>
  export default {
    data() {
      return {
        baseList: [{
            img: require('@/static/icon/healthTreatment/emotion.png'),
            title: '医嘱管理',
            url: '/pages/healthTreatment/doctorAdvice/doctorAdvice'
          },
          {
            img: require('@/static/icon/healthTreatment/medical.png'),
            title: '医疗管理',
            url: '/pages/healthTreatment/medicalTreatment/medicalTreatment'
          },
          { 
            img: require('@/static/icon/healthTreatment/adjust.png'),
            title: '调整管理',
            url: '/pages/healthTreatment/adjustment/adjustment'
          },
          {
            img: require('@/static/icon/healthTreatment/psychology.png'),
            title: '心理调试',
            url: '/pages/healthTreatment/psychology/psychology'
          },
          {
            img: require('@/static/icon/healthTreatment/infrared.png'),
            title: '红外测评',
            url: '/pages/healthTreatment/infrared/infrared'
          },
          {
            img: require('@/static/icon/healthTreatment/fitness.png'),
            title: '健身管理',
            url: '/pages/healthTreatment/fitness/fitness'
          },
          {
            img: require('@/static/icon/healthTreatment/cosmetology.png'),
            title: '美容管理',
            url: '/pages/healthTreatment/cosmetology/cosmetology'
          },
        ]
      };
    },
    //方法
    methods: {

      click(url, name) {
        if (!url) {
          this.$refs.uToast.default('开发中...')
        }
        uni.navigateTo({
          url: url
        });

      }

    },
    onLoad(e) {

    },
    //页面显示
    onShow() {},
  };
</script>

<style lang="scss">
  .content {
    .title {
      text {
        border-left: 8rpx #28be9e solid;
        padding-left: 20rpx;
      }
    }

    .devices-warp {
      .item {
        padding: 20rpx;
        margin: 10rpx;
        width: 160rpx !important;
        border-radius: 16rpx;
        background-color: #fff !important;
        box-shadow: 0px 3px 3px hsla(0, 0, 0, 0.1);

        &:nth-child(4n) {
          margin-right: 0;
        }

        .grid-text {
          font-size: 25rpx;
        }
      }
    }
  }
</style>
