> 官网: [https://haomo-tech.com](https://haomo-tech.com)

> 作者: 毫末科技

> 邮箱: hxg@haomo-studio.com

## 预览

![预览图片](http://downloads.haomo-tech.com/uniapp/hm-photo-card.png)

[在线效果预览](http://template.uniapp.haomo-tech.com/pages/haomo/test-component/hm-photo-card)

更多毫末科技的uni-app跨端模板，请见[毫末科技uni-app跨端模板](https://haomo-tech.com/sale.html)

## 技术支持

* [uni-app插件市场](https://ext.dcloud.net.cn/plugin?id=1404)

* [npm包](https://www.npmjs.com/package/hm-uniapp-photo-card)

* [github地址](https://github.com/haomo-studio/hm-uniapp-photo-card)

* [gitee地址](https://gitee.com/haomo/hm-uniapp-photo-card)

毫末科技将长期迭代本组件。需要技术支持，请进钉钉群：

<img width="250" src="http://downloads.haomo-tech.com/%E6%AF%AB%E6%9C%ABuniapp%E7%BB%84%E4%BB%B6%E6%8A%80%E6%9C%AF%E6%94%AF%E6%8C%81.jpg">

## 概述

毫末uni-app新闻卡片组件。支持H5/小程序(微信、支付宝、头条、百度、QQ)/App；组件可自适应各种屏幕大小的手机。

## 使用

请使用HBuilderX导入组件。

在script中引用：

```javascript
import HmPhotoCard from '@/components/hm-photo-card/index.vue'
export default {
    components: {HmPhotoCard}
}
```

在template中使用：

```html
<template>
  <div class="test-component">
    <hm-photo-card :options="options"></hm-photo-card>
  </div>
</template>
<script>
import HmPhotoCard from '@/components/hm-components/hm-photo-card/index.vue'

export default {
  components: {
    HmPhotoCard
    },
  data() {
    return {
      options: {
          title: '我的 图片',
          titleImg:
            '/static/hm-photo-card/images/img_24027_0_0.png',
          img:
            '/static/hm-photo-card/images/img_24027_0_3.png',
          img1:
            '/static/hm-photo-card/images/img_24027_0_2.png',
          img2:
            '/static/hm-photo-card/images/img_24027_0_4.png',
          img3:
            '/static/hm-photo-card/images/img_24027_0_1.png',
          img4:
            '/static/hm-photo-card/images/img_24027_0_5.png',
          img5:
            '/static/hm-photo-card/images/img_24027_0_6.png'
        }
    };
  },
  methods: {
  }
};
</script>
<style>
</style>





```

## 属性说明

| 属性名        | 类型     | 默认值 | 说明                                                                       |
|-----------   |---------|--------|----------------------------------------------------------------------------|
| options        | Object  | -      | 卡片属性                                                                   |

options对象各个属性说明如下：

| 属性名        | 类型     | 默认值 | 说明                                                                       |
|-----------   |---------|--------|----------------------------------------------------------------------------|
| title        | String  | -      | 标题                                                                  |
| titleImg        | String  | -      | 图片                                                                  |
| img1        | String  | -      | 图片                                                                   |
| img2        | String  | -      | 图片                                                                   |
| img3        | String  | -      | 图片                                                                   |
| img4        | String  | -      | 图片                                                                   |
| img5        | String  | -      | 图片                                                                   |



## 事件说明


## 更新日志

### 0.0.1(2020-03-10)

* 完成第一个版本
