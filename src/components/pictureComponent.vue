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
                            label="导航样式">
                        <a-checkbox :value="2">两列导航</a-checkbox>
                        <a-checkbox :value="3">三列导航</a-checkbox>
                        <a-checkbox :value="4">四列导航</a-checkbox>
                    </a-form-item>
                </a-col>
            </a-row>
            <div>
                <h4>两列导航</h4>
                <div style="padding: 10px; border: 1px solid #eee; margin-bottom: 20px;">
                    <a-row :key="i" v-for="(img,i) in data.listPic[2]">
                        <a-col :span="3">
                            <a-upload
                                    :name="'uploadfile_2_'+i"
                                    :fileList="fileList"
                                    listType="picture-card"
                                    class="avatar-uploader"
                                    :showUploadList="false"
                                    :customRequest="customRequest"
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
                        </a-col>
                    </a-row>



                </div>
            </div>
        </a-form>
    </div>
</template>
<script>
  export default {
    name: 'pictureComponent',
    props: ['data', 'classifyLists', 'jointList'],
    data () {
      return {
        fileList:[]
      }
    },
    methods: {
      blur: function () {

        this.$emit('ok', this.data)
      },
      changeCheck: function (value) {
      },
      beforeUpload:function(){

      },
      customRequest: function (info) {
        var fd = new FormData()
        var url = '/backend/uploadFile/upload_cloud'
        fd.append('fileToUpload',info.file)
        /*this.$http.post(url, fd, {
          emulateJSON: true,
          emulateHTTP: true,
          credentials: true
        }).then(function (res) {
          var bkdata = res.data
          if (bkdata.success) {
            this.data.listPic[type][index].pic_image = bkdata.file_url
          }
        })*/
      },
      changeRadio: function (item) {
        item.pic_type = '3'
      }

    }
  }

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
