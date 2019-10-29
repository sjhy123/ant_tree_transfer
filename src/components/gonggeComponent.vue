<template>
    <div class="component-content">
        <a-form>
            <a-row>
                <a-col :span="24">

                    <a-form-item
                            :label-col="{ span: 3 }" :wrapper-col="{ span: 12 }"
                            label="用途">
                        <a-input
                                v-model="data.use"
                                v-decorator="[
                                  '用途',
                                  {
                                    rules: [
                                      {
                                        required: true,
                                        message: 'Please input your E-mail!',
                                      },
                                    ],
                                  },
                                ]"
                        />
                    </a-form-item>

                    <a-form-item
                            :label-col="{ span: 3 }" :wrapper-col="{ span: 12 }"
                            label="行数">
                        <a-radio-group
                                v-model="data.line" :defaultValue="1"
                        >
                            <a-radio :value="1">1行</a-radio>
                            <a-radio :value="2">2行</a-radio>
                        </a-radio-group>

                    </a-form-item>

                    <a-form-item
                            :label-col="{ span: 3 }" :wrapper-col="{ span: 12 }"
                            label="图标">
                        <a-radio-group
                                v-model="data.showIcon" :defaultValue="1"
                        >
                            <a-radio :value="1">显示</a-radio>
                            <a-radio :value="2">不显示</a-radio>
                        </a-radio-group>
                    </a-form-item>
                    <a-form-item
                            :label-col="{ span: 3 }" :wrapper-col="{ span: 12 }"
                            label="描述">
                        <a-radio-group
                                v-model="data.showIcon" :defaultValue="1"
                        >
                            <a-radio :value="1">显示</a-radio>
                            <a-radio :value="2">不显示</a-radio>
                        </a-radio-group>
                    </a-form-item>

                </a-col>
            </a-row>
            <div style="padding: 10px; border: 1px solid #eee; margin-bottom: 20px;">
                <a-row :key="i" v-for="(img,i) in data.picList">
                    <a-col :span="3">
                        <a-upload
                                name="avatar"
                                listType="picture-card"
                                class="avatar-uploader"
                                :showUploadList="false"
                                action="https://www.mocky.io/v2/5cc8019d300000980a055e76"
                                :beforeUpload="beforeUpload"
                                @change="handleChange"
                        >
                            <img v-if="img.icon_image" :src="img.icon_image" alt="avatar"/>
                            <div v-else>
                                <a-icon type="plus"/>
                                <div class="ant-upload-text">Upload</div>
                            </div>
                        </a-upload>

                    </a-col>
                    <a-col :span="21">
                        <a-form-item
                                :label-col="{ span: 3 }" :wrapper-col="{ span: 12 }"
                                label="描述">
                            <a-input
                                    v-model="data.use"
                                    v-decorator="[
                                  '用途',
                                  {
                                    rules: [
                                      {
                                        required: true,
                                        message: 'Please input your E-mail!',
                                      },
                                    ],
                                  },
                                ]"
                            />

                        </a-form-item>
                        <a-form-item
                                :label-col="{ span: 3 }" :wrapper-col="{ span:20 }"
                                label="投放类型">
                            <a-radio-group

                            >
                                <a-radio :value="1">商品分类</a-radio>
                                <a-radio :value="2">商品组合</a-radio>
                                <a-radio :value="3">秒杀商品</a-radio>
                                <a-radio :value="4">团购商品</a-radio>
                                <a-radio :value="5">优惠券</a-radio>
                                <a-radio :value="6">链接</a-radio>

                            </a-radio-group>

                        </a-form-item>

                        <a-form-item
                                :label-col="{ span: 3 }" :wrapper-col="{ span:12 }"
                                label="角标">
                            <a-input/>
                        </a-form-item>
                        <a-form-item
                                :label-col="{ span: 3 }" :wrapper-col="{ span:12 }"
                                label="排序">
                            <a-input/>
                        </a-form-item>

                    </a-col>
                </a-row>
            </div>
            <a-row>
                <a-col>
                    <a-button @click="addPicture" type="primary">添加一张图片</a-button>
                </a-col>
            </a-row>
        </a-form>


    </div>

</template>
<script>
  export default {
    name: 'gonggeComponent',
    props: ['data', 'classifyLists', 'jointList'],
    data () {
      return {}
    },
    methods: {
      beforeUpload: function () {

      },
      handleChange: function () {

      },
      addPicture: function () {
        if (this.data.picList.length >= 10) {
          return
        }
        this.data.picList.push({
          icon_image: '',
          icon_desc: '',
          icon_type: '1',//1商品分类，2商品组合，3秒杀商品，4团购商品，5优惠券，6链接
          icon_corn: '',
          icon_sort: '0',
          classify_id: '',
          joint_id: '',
          link_url: ''
        })

      },
      changeFile: function (index) {
        var fd = new FormData()
        var url = '/backend/uploadFile/upload_cloud'
        fd.append('fileToUpload', this.$refs['uploadfile_' + index][0].files[0])

        this.$http.post(url, fd, {
          emulateJSON: true,
          emulateHTTP: true,
          credentials: true
        }).then(function (res) {
          var bkdata = res.data
          // this.data.picList[index].icon_image="//img.test.mall.zanjiahao.com//uploadFiles/shopping/cover/20181025/47cc148fac9b5a66ebc2fd1a97d90d9e.jpg-334X334";
          if (bkdata.success) {
            //  this.data.picList[index].icon_image=bkdata.file_url;
            this.data.picList[index].icon_image = bkdata.file_url
          }
        })
      },
      delIconItem: function (index) {
        this.data.picList.splice(index, 1)
      }
    }
  }

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
