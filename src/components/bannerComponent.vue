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
                                :label-col="{ span: 3 }" :wrapper-col="{ span: 21 }"
                                label="类型">
                            <a-col :span="8">
                                <a-radio-group

                                >
                                    <a-radio :value="1">单张</a-radio>
                                    <a-radio :value="1">多张</a-radio>
                                </a-radio-group>
                            </a-col>
                            <a-col :span="6">
                                每&nbsp;
                                <a-input
                                        style="width:50px"
                                        v-model="data.use"
                                />&nbsp;轮播
                            </a-col>
                        </a-form-item>

                        <a-form-item
                                :label-col="{ span: 3 }" :wrapper-col="{ span: 12 }"
                                label="投放分类">
                            <a-select>
                                <a-select-option value="1">1</a-select-option>
                                <a-select-option value="2">2</a-select-option>
                                <a-select-option value="3">3</a-select-option>
                            </a-select>
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
  name: 'bannerComponent',
  props: ['data','classifyLists','jointList'],
  data () {
	return {

      }
	},
	methods: {


      blur: function () {

        this.$emit('ok', this.data);
      },
      changeCheck: function (value) {
        if (!this.data.listPic) {
          this.$set(this.data, 'listPic', {});
        }
        if (!this.data.listPic[value]) {
          this.data.listPic[value] = [];
          for (var i = 0; i < value; i++) {
            this.data.listPic[value].push({})
          }
        }

      },
      changeFile: function (index) {
        var fd = new FormData();
        var url = "/backend/uploadFile/upload_cloud";
        fd.append('fileToUpload', this.$refs["uploadfile_" + index][0].files[0]);

        this.$http.post(url, fd, {
          emulateJSON: true,
          emulateHTTP: true,
          credentials: true
        }).then(function (res) {
          var bkdata=res.data;
          //this.data.picList[index].pic_image="//img.test.mall.zanjiahao.com//uploadFiles/shopping/cover/20181025/47cc148fac9b5a66ebc2fd1a97d90d9e.jpg-334X334";

          if(bkdata.success){
            //  this.data.picList[index].icon_image=bkdata.file_url;
            this.data.picList[index].pic_image=bkdata.file_url;
          }
        })
      },
      addPicture: function () {
        this.data.picList.push({
          pic_desc: '',
          pic_type: '1',
          classify_id:'',
          joint_id:'',
          link_url:'',
          pic_image:''
        })

      },
      delIconItem:function(index){
        this.data.picList.splice(index,1)
      },
      updateSwiper:function(){
        this.$emit('update');
      }
	}
  }

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
