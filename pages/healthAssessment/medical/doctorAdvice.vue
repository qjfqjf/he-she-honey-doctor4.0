<template>
  <view>
    <z-nav-bar title="医嘱">
      <view slot="right" class="p-2" @click="addRecords">
        <image style="width: 40rpx;height: 40rpx;" src="/static/icon/healthAssessment/addRecords.png"></image>
      </view></z-nav-bar>
    <public-module></public-module>
    
    <!-- 内容 -->
    <view class="container">
      <view class="item" v-for="(item, index) in baseList" :key="index">
        <view class="public name">{{item.name}}</view>
        <view class="public content">内容：{{item.content}}</view>
        <view class="public date">时间：{{item.date}}</view>
        <view class="public remarks">备注：{{item.remarks}}</view>
      </view>
    </view>
  </view>
</template>

<script>
  export default {
    data() {
      return {
        baseList: [
          // {
          //   name: '彭老师',
          //   content: '鹏辉你血压很高,明天到我这来复诊。',
          //   date: '2022-09-24 19:33:00',
          //   remarks: '一定记得'
          // }, {
          //   name: '平台管理员',
          //   content: '鹏辉你血压很高,明天到我这来复诊。',
          //   date: '2022-09-24 19:33:00',
          //   remarks: ''
          // }, {
          //   name: '李老师',
          //   content: '鹏辉你血压很高,明天到我这来复诊。',
          //   date: '2022-09-24 19:33:00',
          //   remarks: '一定记得'
          // },
        ],
        data:{}
      };
    },
    onLoad: function (option) {
          // this.getDoctorAdvice()
      },
    methods:{
      addRecords(){
        uni.navigateTo({
          url:'/pages/healthAssessment/medical/addSymptomSelfReport?type=' + 1
        })
      },
      getDoctorAdvice(){
        this.$http.post('/medical_file/index',{
          type:1
        }).then((res)=>{
          res.data.data.forEach(element => {
            const newData = {};
            newData.name = element.fullname;
            newData.content = element.symptom;
            newData.date = element.time;
            newData.remarks = element.way;
            this.baseList.push(newData);
          });
        })
      }
    }
  }
</script>

<style lang="scss">
.container{
  .item{
    background-color: white;
    margin: 16rpx 0;
    padding: 30rpx;
    font-size: 30rpx;
    .public{
      margin: 14rpx;
    }
  }
}
</style>
