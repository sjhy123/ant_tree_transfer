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
                        label="显示商品个数">
                    <a-input
                            v-model="data.use"
                            v-decorator="[
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
                        label="背景图">
                    <a-upload
                            listType="picture-card"
                            class="avatar-uploader"
                            :showUploadList="false"
                    >
                       <!-- <img v-if="img.icon_image" :src="img.icon_image" alt="avatar"/>-->
                        <div >
                            <a-icon type="plus"/>
                            <div class="ant-upload-text">Upload</div>
                        </div>
                    </a-upload>

                </a-form-item>

                <a-form-item
                        :label-col="{ span: 3 }" :wrapper-col="{ span: 12 }"
                        label="选择商品">
                    <a-select>
                        <a-select-option value="1">商品分类</a-select-option>
                        <a-select-option value="2">商品组合</a-select-option>
                    </a-select>

                </a-form-item>
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
	methods:  {
      blur: function () {

        this.$emit('ok', this.data);
      },
      blurLimit:function(){
        if(!this.data.limit_num||this.data.limit_num<3){
          this.data.limit_num=3
        }
      },
      changeFile: function () {
        var fd = new FormData();
        var url = "/backend/uploadFile/upload_cloud";
        fd.append('fileToUpload', this.$refs["uploadfile"].files[0]);
        this.$http.post(url, fd, {
          emulateJSON: true,
          emulateHTTP: true,
          credentials: true
        }).then(function (res) {
          var bkdata=res.data;
          // this.data.bg_image="//img.test.mall.zanjiahao.com//uploadFiles/shopping/cover/20181025/47cc148fac9b5a66ebc2fd1a97d90d9e.jpg-334X334";
          if(bkdata.success){
            //  this.data.picList[index].icon_image=bkdata.file_url;
            this.data.bg_image=bkdata.file_url;
          }
        })
      }

    }
  }

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
