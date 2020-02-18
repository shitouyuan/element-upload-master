# 目的

- 本项目的目的是教你如何实现一个封装的图片上传组件
- 本项目中已经封装的图片上传组件可以拿来即用引入到自己项目中
- 本项目插件可以自行扩展实现


本项目的图像文件来自于网图链接。

# 运行
```
进入到项目目录执行如下：
npm install
npm run dev
```

# 文档
# 1. 简介
## 1.1 相关技术

- [Vue](https://cn.vuejs.org/)
- [Vue-cli](https://github.com/vuejs/vue-cli)
- [ElementUI](http://element-cn.eleme.io/#/zh-CN)


## 1.2 从本教程你会学到什么？

- `图片上传组件的封装`
- `Element UI基本用法`
- `组件引用及使用方法`
- `直接拿来即用的组件`


## 1.3 如何引入到自己的项目中
### 1.31 复制如下路径的组件文件：
/src/components/pic-upload
放至自己的专门存放组件的文件夹中

### 1.32 在需要引入组件.vue文件中进行引入
import PicUpload from './components/pic-upload/pic-upload'

### 1.33 进行组件的声明
export default {
  name: 'app',
  // 进行组件的声明
  components: {
    PicUpload
  },
  }
  
### 1.34 直接进行使用
 <PicUpload v-model="viewImgss"
               :isUpload="isUpload3"
               :maxPicNum="5"
               :uploadUrl="uploadUrl">
	</PicUpload>



## 参考文档
- [ElementUI 上传组件使用说明](https://element.eleme.cn/#/zh-CN/component/upload)
- [Vue.js文档](https://cn.vuejs.org/)
