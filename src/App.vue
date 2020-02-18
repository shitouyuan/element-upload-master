<template>
  <div id="app">
    <span>图片预览模式（单图）</span>
    <PicUpload v-model="viewImg"
               :isUpload="isUpload2"
               :maxPicNum="5"
               :uploadUrl="uploadUrl"></PicUpload>
    <br><br>
    <span>图片预览模式（多图）</span>
    <PicUpload v-model="viewImgs"
               :isUpload="isUpload2"
               :maxPicNum="5"
               :uploadUrl="uploadUrl"></PicUpload>
    <br><br>
    <span>图片上传模式</span>
    <PicUpload v-model="viewImgss"
               :isUpload="isUpload3"
               :maxPicNum="5"
               :uploadUrl="uploadUrl"></PicUpload>
  </div>
</template>

<script>
// 进行组件的引用
import PicUpload from './components/pic-upload/pic-upload'

export default {
  name: 'app',
  // 进行组件的声明
  components: {
    PicUpload
  },
  data () {
    return {
      // true为上传模式   false为预览模式
      // 上传使用true  查看图片使用false
      isUpload2: false,
      isUpload3: true,
      // 服务器上传接口
      uploadUrl: '/api/upload?bizType=treeInfo',
      // 图片链接数组，支持多图多链接[{ url: "http://t8.baidu.com/it/u=1484500186,1503043093&fm=79&app=86&size=h300&n=0&g=4n&f=jpeg?sec=1582627321&t=feca81628f9c6e1fe09ab5e66a1e5a05" }],
      viewImg: [{ url: "http://t8.baidu.com/it/u=1484500186,1503043093&fm=79&app=86&size=h300&n=0&g=4n&f=jpeg?sec=1582627321&t=feca81628f9c6e1fe09ab5e66a1e5a05" }],
      viewImgs: [{ url: "http://t8.baidu.com/it/u=1484500186,1503043093&fm=79&app=86&size=h300&n=0&g=4n&f=jpeg?sec=1582627321&t=feca81628f9c6e1fe09ab5e66a1e5a05" }, { url: "http://t8.baidu.com/it/u=1484500186,1503043093&fm=79&app=86&size=h300&n=0&g=4n&f=jpeg?sec=1582627321&t=feca81628f9c6e1fe09ab5e66a1e5a05" }, { url: "http://t8.baidu.com/it/u=1484500186,1503043093&fm=79&app=86&size=h300&n=0&g=4n&f=jpeg?sec=1582627321&t=feca81628f9c6e1fe09ab5e66a1e5a05" }, { url: "http://t8.baidu.com/it/u=1484500186,1503043093&fm=79&app=86&size=h300&n=0&g=4n&f=jpeg?sec=1582627321&t=feca81628f9c6e1fe09ab5e66a1e5a05" }],
      viewImgss: []
    }
  }
}
</script>

<style>
</style>
