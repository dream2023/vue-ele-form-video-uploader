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
  // 对所有具有上传属性的组件适用
  upload: {
    fileSize: 10
  },
  // 可以在这里设置全局的 video-uploader 属性
  // 具体属性列表请看下面 #attrs
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
    // 只需要在这里指定为 video-uploader 即可
    type: 'video-uploader',
    // 具体属性列表请看下面 #attrs
    attrs: {
      action: 'https://jsonplaceholder.typicode.com/posts', // 上传地址
      data: { token: 'xxx' }, // 附带数据
      // 上传后对响应处理, 拼接为一个视频的地址
      handleResponse(response, file) {
        // 根据响应结果, 设置 URL
        return 'https://xxx.xxx.com/video/' + response.id
      }
    }
  }
}
```

## 示例

```html
<template>
  <el-card
    header="ele-form-image-uploader 演示"
    shadow="never"
    style="max-width: 1250px;margin: 20px auto;"
  >
    <ele-form
      :form-data="formData"
      :form-desc="formDesc"
      :request-fn="handleRequest"
      @request-success="handleSuccess"
    />
  </el-card>
</template>

<script>
export default {
  data () {
    return {
      formData: {},
      formDesc: {
        video: {
          label: '团队介绍',
          type: 'video-uploader',
          attrs: {
            fileSize: 20,
            action: 'https://jsonplaceholder.typicode.com/posts',
            responseFn (response, file) {
              return URL.createObjectURL(file.raw)
            }
          }
        }
      }
    }
  },
  methods: {
    handleRequest (data) {
      console.log(data)
      return Promise.resolve()
    },
    handleSuccess () {
      this.$message.success('提交成功')
    }
  },
  mounted () {}
}
</script>

<style>
body {
  background-color: #f0f2f5;
}
</style>
```

## attrs

> 属性具体参考: [vue-ele-upload-video](https://github.com/dream2023/vue-ele-upload-video)

```js
attrs: {
  // 上传地址
  action: {
    type: String,
    required: true
  },
  // 响应处理函数
  responseFn: Function,
  // 文件大小限制(Mb)
  fileSize: {
    type: Number
  },
  // 显示宽度(px)
  width: {
    type: Number,
    default: 360
  },
  // 显示高度(默认auto)
  height: {
    type: Number
  },
  // 是否显示提示
  isShowTip: {
    type: Boolean,
    default: true
  },
  // 文件类型
  fileType: {
    type: Array
  },
    // 设置上传的请求头部(同官网)
  headers: Object,
  // 支持发送 cookie 凭证信息 (同官网)
  withCredentials: {
    type: Boolean,
    default: false
  },
  // 上传时附带的额外参数(同官网)
  data: {
    type: Object
  },
  // 上传的文件字段名 (同官网)
  name: {
    type: String,
    default: 'file'
  },
    // 覆盖默认的上传行为，可以自定义上传的实现 (同官网)
  httpRequest: Function,
  // 接受上传的文件类型（thumbnail-mode 模式下此参数无效）(同官网)
  accept: String
}
```

## 相关链接

- [vue-ele-upload-video](https://github.com/dream2023/vue-ele-upload-video)
- [vue-ele-form](https://github.com/dream2023/vue-ele-form)
- [element-ui](http://element-cn.eleme.io)
