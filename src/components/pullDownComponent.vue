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
  name: 'pullDownComponent',
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
        if(!this.data.limit_num||this.data.limit_num<0){
          this.data.limit_num=0
        }
      },
      changeCheck: function (value) {

      }

    }
  }

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
