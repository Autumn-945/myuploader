
# 基于Vue-element-template项目实现基于vue-simple-uploader封装文件分片上传、秒传及断点续传的全局上传插件

最近做一个视频存储的项目，使用了Vue-element-template模板进行整合，其中有一个需求是做一个视频上传的断点续传功能，经过查询资料做出来了，过程如下：

首先：先安装vue-simple-uploader插件，然后在main.js中引入使用。

**安装：**`npm install vue-simple-uploader --save**`**

**使用：**

```
import uploader from 'vue-simple-uploader'
Vue.use(uploader)
```

然后引入common,components文件夹，讲这两个文件夹放到一个自己建好的uploader文件夹中。

然后在与uploader文件夹同级下的index.vue文件中使用下面的代码即可

```
<template>
  <div>
    <uploader :options="options" :file-status-text="statusText" class="uploader-example" ref="uploader" @file-complete="fileComplete" @complete="complete"></uploader>
  </div>
</template>

<script>
  export default {
    data () {
      return {
        options: {
          target: 'http://120.24.78.29:8086/video/upload', // '//jsonplaceholder.typicode.com/posts/',
          testChunks: false
        },
        attrs: {
          accept: 'image/*'
        },
        statusText: {
          success: '成功了',
          error: '出错了',
          uploading: '上传中',
          paused: '暂停中',
          waiting: '等待中'
        }
      }
    },
    methods: {
      complete () {
        console.log('complete', arguments)
      },
      fileComplete () {
        console.log('file complete', arguments)
      }
    },
    mounted () {
      this.$nextTick(() => {
        window.uploader = this.$refs.uploader.uploader
      })
    }
  }
</script>

<style>
  .uploader-example {
    width: 880px;
    padding: 15px;
    margin: 40px auto 0;
    font-size: 12px;
    box-shadow: 0 0 10px rgba(0, 0, 0, .4);
  }
  .uploader-example .uploader-btn {
    margin-right: 4px;
  }
  .uploader-example .uploader-list {
    max-height: 440px;
    overflow: auto;
    overflow-x: hidden;
    overflow-y: auto;
  }
</style>

```

参考如下链接：

[](https://www.cnblogs.com/xiahj/p/vue-simple-uploader.html)

最后附上源码：

