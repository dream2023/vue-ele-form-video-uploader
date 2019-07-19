# vue-ele-form-video-uploader | vue-ele-form 的视频上传扩展组件

[![MIT Licence](https://badges.frapsoft.com/os/mit/mit.svg)](https://opensource.org/licenses/mit-license.php)
[![npm](https://img.shields.io/npm/v/vue-ele-form-video-uploader.svg)](https://www.npmjs.com/package/vue-ele-form-video-uploader)
[![download](https://img.shields.io/npm/dw/vue-ele-form-video-uploader.svg)](https://npmcharts.com/compare/vue-ele-form-video-uploader?minimal=true)

## 介绍

vue-ele-form-video-uploader 做为 vue-ele-form 的第三方扩展, 通过对 [vue-ele-upload-video](https://github.com/dream2023/vue-ele-upload-video) 的封装, 大大优化了视频上传的体验

![image](https://raw.githubusercontent.com/dream2023/images/master/vue-ele-form-video-uploader.czl72wc81hq.gif)

## 安装

```bash
npm install vue-ele-form-video-uploader --save
```

## 使用

```js
import EleForm from 'vue-ele-form'
import EleFormVideoUploader from 'vue-ele-form-video-uploader'
// 注册 ele-form
Vue.use(EleForm, {
  // 可以在这里设置全局的 video-uploader 属性
  'video-uploader': {
    action: 'https://jsonplaceholder.typicode.com/posts' // 上传地址
  }
})

// 注册 video-uploader 组件
Vue.component('video-uploader', EleFormVideoUploader)
```

```js
formDesc: {
  xxx: {
    label: 'xxx',
    type: 'video-uploader', // 只需要在这里指定为 video-uploader 即可
    // 属性参考: https://github.com/dream2023/vue-ele-upload-video
    attrs: {
      action: 'https://jsonplaceholder.typicode.com/posts', // 上传地址
      data: {token: 'xxx'}, // 附带数据
      // 上传后对响应处理, 拼接为一个视频的地址
      handleResponse(response, file) {
        // 根据响应结果, 设置 URL
        return 'https://xxx.xxx.com/video/' + response.id
      }
    }
  }
}
```

## 相关链接

- [vue-ele-upload-video](https://github.com/dream2023/vue-ele-upload-video)
- [vue-ele-form](https://github.com/dream2023/vue-ele-form)
- [element-ui](http://element-cn.eleme.io)
