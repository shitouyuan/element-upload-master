<template>
  <div>
    <div :key="index"
         class="demo-upload-list"
         v-for="(item,index) in uploadList">
      <template v-if="item.status === 'finished'">
        <img :src="uploadServiceName+item.url">
        <div class="demo-upload-list-cover">
          <!-- ele i ivew Icon -->
          <!-- ele class  iview type -->
          <i class="el-icon-view"
             @click="handleView(item)"></i>
          <i v-if="isUpload"
             class="el-icon-delete"
             @click="handleRemove(item)"></i>
        </div>
      </template>
      <template v-else>
        <Progress v-if="item.showProgress"
                  :percent="item.percentage"
                  hide-info></Progress>
      </template>
    </div>
    <el-upload ref="upload"
               v-show="showUpload"
               :show-upload-list="false"
               :default-file-list="defaultList"
               :on-success="handleSuccess"
               :format="['jpg','jpeg','png']"
               :max-size="maxFileSize"
               :on-format-error="handleFormatError"
               :on-exceeded-size="handleMaxSize"
               :before-upload="handleBeforeUpload"
               multiple
               type="drag"
               :action="uploadServiceName+uploadUrl"
               style="display: inline-block;width:58px;">
      <div style="width: 58px;height:58px;line-height: 58px; font-size:70px">
        <!-- ele i ivew Icon -->
        <i class="el-icon-plus"
           size="500"></i>
      </div>
    </el-upload>
    <el-dialog title="查看图片"
               :visible.sync="visible">
      <img :src="viewPicUrl"
           v-if="visible"
           style="width: 100%">
    </el-dialog>
  </div>
</template>
<script>
export default {
  name: 'PicUpload',
  props: {
    /**
       * 图片数组
       * */
    value: {
      type: Array,
      default () {
        return []
      }
    },
    /**
       * 图片上传数量控制参数,默认是上传6张图片
       * */
    maxPicNum: {
      type: Number,
      default: 6
    },
    /**
       * 文件上传路径
       * */
    uploadUrl: {
      type: String,
      default: ''
    },
    /**
       * 是否是上传类型, false则为查看
       */
    isUpload: {
      type: Boolean,
      default: true
    },
    maxFileSize: {
      type: Number,
      default: 20480
    }
  },
  data () {
    return {
      imgName: '',
      visible: false,
      showUpload: true,
      viewPicUrl: '',
      defaultList: [],
      uploadList: [],
      uploadServiceName: '' // 上传服务器前缀，这里可以为空
    }
  },
  methods: {
    handleView (file) {  //预览查看图片方法
      this.viewPicUrl = this.uploadServiceName + file.url
      this.visible = true
    },
    handleRemove (file) {  //添加图片中可以将图片删除
      const fileList = this.$refs.upload.fileList
      this.$refs.upload.fileList.splice(fileList.indexOf(file), 1)
      this.uploadList = this.$refs.upload.fileList
      if (this.isUpload && this.uploadList.length < this.maxPicNum) {
        this.showUpload = true
      }
    },
    handleSuccess (res, file) { //成功上传回调处理
      file.url = file.response.data.fileUrl
      this.uploadList = this.$refs.upload.fileList
      if (this.isUpload && this.uploadList.length >= this.maxPicNum) {
        this.showUpload = false
      }
    },
    handleFormatError (file) {  //格式校验不正确
      this.$Notice.warning({
        title: '图片格式不正确',
        desc: '图片 ' + file.name + ' 的格式不正确,请选择 jpg, png, jpeg.'
      })
    },
    handleMaxSize (file) {
      this.$Notice.warning({
        title: '文件大小超过限制',
        desc: '文件  ' + file.name + ' 太大, 不能超过 ' + this.maxFileSize / 1024 + 'M.'
      })
    },
    handleBeforeUpload () {  // 上传数量校验
      const check = this.$refs.upload.fileList.length < this.maxPicNum
      if (!check) {
        this.$Notice.warning({
          title: '超过最大上传数量'
        })
      }
      return check
    },
    init () {
      this.value.forEach(item => {
        item.status = 'finished'
        item.name = item.url
      })
      this.defaultList = this.value
      this.uploadList = this.value
      this.showUpload = true
      if (!this.isUpload) {
        this.showUpload = false
      } else if (this.isUpload && this.value.length >= this.maxPicNum) {
        this.showUpload = false
      }
    }
  },
  mounted () {
    this.init()
  },
  watch: {
    value (val) {
      this.init()
    }
  }
}
</script>
<style scoped>
.demo-upload-list {
  display: inline-block;
  width: 60px;
  height: 60px;
  text-align: center;
  line-height: 60px;
  border: 1px solid transparent;
  border-radius: 4px;
  overflow: hidden;
  background: #fff;
  position: relative;
  box-shadow: 0 1px 1px rgba(0, 0, 0, 0.2);
  margin-right: 4px;
}
.demo-upload-list img {
  width: 100%;
  height: 100%;
}
.demo-upload-list-cover {
  display: none;
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background: rgba(0, 0, 0, 0.6);
}
.demo-upload-list:hover .demo-upload-list-cover {
  display: block;
}
.demo-upload-list-cover i {
  color: #fff;
  font-size: 20px;
  cursor: pointer;
  margin: 0 2px;
}
</style>