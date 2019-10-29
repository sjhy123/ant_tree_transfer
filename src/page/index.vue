<template>
 <div class="" style='width:1200px;margin:0 auto;'>
     <a-row :gutter="20">
         <a-col :span="6">
             <div class="left-content">
                 <h4 class="title">组件库</h4>
                 <div id='left-defaults' style="min-height: 800px; background: #fff">
                     <div class="left-component" drop="false" style="color:#999; padding-left: 20px">banner顶部</div>
                     <div class="left-component" label="gongge"><img style="width:12px; vertical-align: -2px; opacity: 0.65;margin-right: 8px;" src="/static/images/icon_tuodong@3x.svg" />宫格导航</div>
                     <div class="left-component" label="picture"><img style="width:12px; vertical-align: -2px; opacity: 0.65;margin-right: 8px; " src="/static/images/icon_tuodong@3x.svg" />图片导航</div>
                     <div class="left-component" label="banner"><img style="width:12px; vertical-align: -2px; opacity: 0.65;margin-right: 8px; " src="/static/images/icon_tuodong@3x.svg" />自定义banner</div>
                     <div class="left-component" drop="false" >商品列表<i class="icon-show icon-show-right"></i></div>
                     <div class="left-component t24" label="goods_pulldown" ><img style="width:12px; vertical-align: -2px; opacity: 0.65;margin-right: 8px; " src="/static/images/icon_tuodong@3x.svg" />瀑布流</div>
                     <div class="left-component t24" label="goods_leftright" ><img style="width:12px; vertical-align: -2px; opacity: 0.65;margin-right: 8px;" src="/static/images/icon_tuodong@3x.svg" />左右滚动</div>
                     <div class="left-component" label="tuan"><img style="width:12px; vertical-align: -2px; opacity: 0.65;margin-right: 8px;" src="/static/images/icon_tuodong@3x.svg" />团购</div>
                     <div class="left-component" label="skill"><img style="width:12px; vertical-align: -2px; opacity: 0.65;margin-right: 8px;" src="/static/images/icon_tuodong@3x.svg" />秒杀</div>
                     <div class="left-component" drop="false" style="color:#999; padding-left: 20px">热门推荐</div>
                 </div>
             </div>
         </a-col>
         <a-col :span="18" class="center-content">
                 <div id="right-defaults" style="min-height:400px;">
                     <div
                             v-for="(items,index) in componentList"
                             v-if="items.componentName=='gongge'"
                             :time="items.time"
                             :order="items.order"
                             :class="['component-list gongge-component validationEngineContainer','validationEngineContainer'+items.time]"
                     >

                         <div class="head clearfix">
                             <div style="cursor: pointer" @click="toggleShow(items)"
                                  class="pull-left">{{items.order+1}}、宫格导航<i
                                     :class="['icon-show',{'icon-show-down':items.showCon}]"></i>
                             </div>
                             <div class="pull-right">
                                 <i @click="changeIndexShow(items)"
                                    :class="['web-font fa fa-eye view-detail',{grayColor:!items.indexShow}] "></i>
                                 <i @click="delComponent(items)" class="web-font fa fa-trash "></i>
                             </div>
                         </div>
                         <div class="component-body" v-show="items.showCon">
                             <!---->
                             <gongge-component  :classifyLists="classifyLists" :jointList="jointList" :data='items' @ok='ok'></gongge-component>
                         </div>

                     </div>

                     <div v-else-if="items.componentName=='picture'"
                          :time="items.time"
                          :order="items.order"
                          :class="['component-list picture-component validationEngineContainer','validationEngineContainer'+items.time]"
                     >


                         <div class="head clearfix">
                             <div style="cursor: pointer" @click="toggleShow(items)"
                                  class="pull-left">{{items.order+1}}、图片导航<i
                                     :class="['icon-show',{'icon-show-down':items.showCon}]"></i>
                             </div>
                             <div class="pull-right">
                                 <i @click="changeIndexShow(items)"
                                    :class="['web-font fa fa-eye view-detail',{grayColor:!items.indexShow}] "></i>
                                 <i @click="delComponent(items)" class="web-font fa fa-trash "></i>
                             </div>
                         </div>
                         <div class="component-body" v-show="items.showCon">
                             <picture-component :classifyLists="classifyLists" :jointList="jointList" :data='items' @ok='ok'/>
                         </div>
                     </div>

                     <div v-else-if="items.componentName=='banner'"
                          :class="['component-list banner-component validationEngineContainer','validationEngineContainer'+items.time]"
                          :time="items.time"
                          :order="items.order"
                     >

                         <div class="head clearfix">
                             <div style="cursor: pointer" @click="toggleShow(items)"
                                  class="pull-left">{{items.order+1}}、自定义banner<i
                                     :class="['icon-show',{'icon-show-down':items.showCon}]"></i>
                             </div>
                             <div class="pull-right">
                                 <i @click="changeIndexShow(items)"
                                    :class="['web-font fa fa-eye view-detail',{grayColor:!items.indexShow}] "></i>
                                 <i @click="delComponent(items)" class="web-font fa fa-trash "></i>
                             </div>
                         </div>
                         <div class="component-body" v-show="items.showCon">
                             <banner-component :classifyLists="classifyLists" :jointList="jointList" :data='items' @update='initSwiper'/>
                         </div>
                     </div>

                     <div v-else-if="items.componentName=='skill'"
                          :class="['component-list skill-component validationEngineContainer','validationEngineContainer'+items.time]"
                          :time="items.time"
                          :order="items.order"
                     >

                         <div class="head clearfix">
                             <div style="cursor: pointer" @click="toggleShow(items)"
                                  class="pull-left">{{items.order+1}}、秒杀
                             </div>
                             <div class="pull-right">
                                 <i @click="changeIndexShow(items)"
                                    :class="['web-font fa fa-eye view-detail',{grayColor:!items.indexShow}] "></i>
                                 <i @click="delComponent(items)" class="web-font fa fa-trash "></i>
                             </div>
                         </div>
                     </div>

                     <div v-else-if="items.componentName=='tuan'"
                          :class="['component-list tuan-component validationEngineContainer','validationEngineContainer'+items.time]"
                          :time="items.time"
                          :order="items.order"
                     >
                         <div class="head clearfix">
                             <div style="cursor: pointer" @click="toggleShow(items)"
                                  class="pull-left">{{items.order+1}}、团购
                             </div>
                             <div class="pull-right">
                                 <i @click="changeIndexShow(items)"
                                    :class="['web-font fa fa-eye view-detail',{grayColor:!items.indexShow}] "></i>
                                 <i @click="delComponent(items)" class="web-font fa fa-trash "></i>
                             </div>
                         </div>
                     </div>

                     <div v-else-if="items.componentName=='goods_pulldown'"
                          :class="['component-list goods_pulldown-component validationEngineContainer','validationEngineContainer'+items.time]"
                          :time="items.time"
                          :order="items.order"
                     >
                         <div class="head clearfix">
                             <div style="cursor: pointer" @click="toggleShow(items)"
                                  class="pull-left">{{items.order+1}}、商品列表(瀑布流)<i
                                     :class="['icon-show',{'icon-show-down':items.showCon}]"></i>
                             </div>
                             <div class="pull-right">
                                 <i @click="changeIndexShow(items)"
                                    :class="['web-font fa fa-eye view-detail',{grayColor:!items.indexShow}] "></i>
                                 <i @click="delComponent(items)" class="web-font fa fa-trash "></i>
                             </div>
                         </div>
                         <div class="component-body" v-show="items.showCon">
                             <pull-down-component :classifyLists="classifyLists" :jointList="jointList" :data='items' @ok='ok'/>
                         </div>
                     </div>

                     <div v-else-if="items.componentName=='goods_leftright'"
                          :class="['component-list goods_leftright-component validationEngineContainer','validationEngineContainer'+items.time]"
                          :time="items.time"
                          :order="items.order"
                     >
                         <div class="head clearfix">
                             <div style="cursor: pointer" @click="toggleShow(items)"
                                  class="pull-left">{{items.order+1}}、商品列表(左右滚动)<i
                                     :class="['icon-show',{'icon-show-down':items.showCon}]"></i>
                             </div>
                             <div class="pull-right">
                                 <i @click="changeIndexShow(items)"
                                    :class="['web-font fa fa-eye view-detail',{grayColor:!items.indexShow}] "></i>
                                 <i @click="delComponent(items)" class="web-font fa fa-trash "></i>
                             </div>
                         </div>
                         <div class="component-body" v-show="items.showCon">
                             <left-right-component  :classifyLists="classifyLists" :jointList="jointList" :data='items' @ok='ok'/>
                         </div>
                     </div>
             </div>
         </a-col>
     </a-row>
 </div>
</template>
<script>
import gonggeComponent from '../components/gonggeComponent'
import pictureComponent from '../components/pictureComponent'
import bannerComponent    from '../components/bannerComponent'
import leftRightComponent    from '../components/leftRightComponent'
import pullDownComponent    from '../components/pullDownComponent'
import dragula  from 'dragula'

export default {
	  name: 'index',
      components:{
        gonggeComponent,
        pictureComponent,
        bannerComponent,
        leftRightComponent,
        pullDownComponent
      },
  data(){
	    return {
          test:1,
          module_type:0,//0系统模板，1社区模板
          mid:0,//0系统模板，1社区模板
          copy_id:1,
          module_name:"",
          village_id:"",
          componentList: [
            {
              componentName: 'hotGoods',
              indexShow: true,
              order: 999
            }],
          classifyLists:[],
          jointList:[],
          provinceList: [],
          cityList: [],
          checkedPro: {
            province_id: '',
            province_name: ''
          },
          checkedCity: {
            cityID: '',
            name: ''
          },
          checkedVillage:[]
        }
  },
  mounted: function () {
    this.init();

  },
  methods: {

    toggleShow: function (items) {
      items.showCon = !items.showCon
    },

    ok: function (data) {
      this.data = data;
    },

    init: function () {
      var _this = this;
      var right = document.getElementById('right-defaults')
      //var left=document.getElementById('left-defaults')
      var left = document.getElementById('left-defaults')
      var drake = dragula([left, right], {
        isContainer: function (el) {
          return false;
          // only elements in drake.containers will be taken into account
        },
        moves: function (el, source, handle, sibling) {
          //&&$(handle).parents('.content').attr('drop')!='false'
          return el.getAttribute('drop') != "false";
          // return el.getAttribute('drop')!="false"&&$(handle).parents('.content').attr('drop')!='false'; // elements are always draggable by default
        },
        accepts: function (el, target, source, sibling) {
          return target != left; // elements can be dropped in any of the `containers` by default
        },
        invalid: function (el, handle) {

          return false; // don't prevent any drags from initiating by default
        },
        direction: 'vertical',             // Y axis is considered when determining where an element would be dropped
        copy: function (el, source) {
          return source === left
        },                       // elements are moved by default, not copied
        copySortSource: false,             // elements in copy-source containers can be reordered
        revertOnSpill: false,              // spilling will put the element back where it was dragged from, if this is true
        removeOnSpill: false,              // spilling will `.remove` the element, if this is true
        mirrorContainer: document.body,    // set the element that gets mirror elements appended
        ignoreInputTextSelection: true     // allows users to select input text, see details below
      }).on('dragend',function(){
        drake.remove();
      }).on('drag', function (el) {


      }).on('drop', function (el, target, source, sibling) {
        var label = el.getAttribute('label');

        if (source.getAttribute('id') == 'left-defaults' && target == right) {
          var order =Array.prototype.indexOf.call(el.parentNode.children, el);
         // var order = $(el).index($(this).parent().parent()[0]);
          //匹配标签，并且从左边拉动

          drake.remove();

          switch (label) {
            case 'gongge':
              _this.componentList.push({
                componentName: 'gongge',
                order: order,
                showCon: true,//显示内容,
                indexShow: true,
                time: new Date().getTime(),
                use: '',
                line: '1',
                showDesc: '1',
                showIcon: '1',
                picList: [{
                  icon_image: '',
                  icon_desc: '',
                  icon_type: '1',//1商品分类，2商品组合，3秒杀商品，4团购商品，5优惠券，6链接
                  icon_corn: '',
                  icon_sort: '0',
                  classify_id:'',
                  joint_id:"",
                  link_url:''
                }]
              });
              break;
            case 'picture':
              _this.componentList.push({
                componentName: 'picture',
                order: order,
                showCon: true,//显示内容
                indexShow: true,
                time: new Date().getTime(),
                picType: [],
                listPic: {
                  2: [{pic_type: "1",pic_image:'',classify_id:'',joint_id:"",link_url:""}, {pic_type: "1",pic_image:'',classify_id:'',joint_id:"",link_url:""}],
                  3: [{pic_type: "1",pic_image:'',classify_id:'',joint_id:"",link_url:""}, {pic_type: "1",pic_image:'',classify_id:'',joint_id:"",link_url:""}, {pic_type: "1",pic_image:'',classify_id:'',joint_id:"",link_url:""}],
                  4: [{pic_type: "1",pic_image:'',classify_id:'',joint_id:"",link_url:""}, {pic_type: "1",pic_image:'',classify_id:'',joint_id:"",link_url:""}, {pic_type: "1",pic_image:'',classify_id:'',joint_id:"",link_url:""}, {pic_type: "1",pic_image:'',classify_id:'',joint_id:"",link_url:""}]
                }
              })
              break;
            case 'banner':
              _this.componentList.push({
                componentName: 'banner',
                order: order,
                showCon: true,//显示内容
                indexShow: true,
                time: new Date().getTime(),
                use: '',
                type: "1",
                speed: '3',
                picList: [{
                  pic_desc: '',
                  pic_type: '1',
                  classify_id:'',
                  joint_id:'',
                  link_url:'',
                  pic_image:''
                }]
              })
              break;
            case 'goods_pulldown':
              _this.componentList.push({
                componentName: 'goods_pulldown',
                order: order,
                showCon: true,//显示内容
                indexShow: true,
                time: new Date().getTime(),
                use: '',
                main_title: '',
                second_titile: '',
                line_type: '2',
                limit_num: '3',
                showMore: "1",
                goods_type: '1',//1商品分类，2商品组合
                classify_id:'',
                joint_id:'',
              })
              break;
            case 'goods_leftright':
              _this.componentList.push({
                componentName: 'goods_leftright',
                order: order,
                showCon: true,//显示内容
                indexShow: true,
                time: new Date().getTime(),
                use: '',
                main_title: '',
                second_titile: '',
                limit_num: '3',
                showMore: '1',
                goods_type: '1',//1商品分类，2商品组合
                classify_id:'',
                joint_id:'',
                bg_image:''
              })
              break;
            case 'tuan':
              _this.componentList.push({
                componentName: 'tuan',
                indexShow: true,
                order: order,
                time: new Date().getTime(),
              })
              break;
            case 'skill':
              _this.componentList.push({
                componentName: 'skill',
                order: order,
                indexShow: true,
                time: new Date().getTime(),
              })
              break;
          }

          _this.componentList.sort(function(a,b){
            if(parseInt(a.order)===parseInt(b.order)){
              return  parseInt(b.time)-parseInt(a.time)
            }
            return parseInt(a.order)-parseInt(b.order)
          });
          _this.componentList.forEach(function(row,i){
            if(row.componentName!="hotGoods")
              row.order=i;
          })
          _this.resetOrder()
        }

        if (source.getAttribute('id') == 'right-defaults') {
          _this.resetOrder()
        }
      })
    },
    subData: function () {
      this.componentList.forEach(function (row) {
        if (row.componentName == "gongge") {
          row.picList = row.picList.sort(function (a, b) {
            return parseInt(b.icon_sort, 10) - parseInt(a.icon_sort, 10)
          })
        }
      });

      var url="";

      var params={
        module_type:this.module_type,
        module_name:this.module_name,
        village_id:$("#select_village").val(),
        content:JSON.stringify(this.componentList),
        getVillageByCityID:1
      };
      if(this.mid){
        url="/backend/yard/edit";
        params.mid=this.mid;
      }else{
        url="/backend/yard/add"
      }
      this.$http.post(url, params, {
        emulateJSON: true,
        emulateHTTP: true,
        credentials: true
      }).then(function (res) {
        if (res.data.success == true) {
          layer.msg(res.data.msg,{
            time:1000,
            end:function(){
              window.location.href="/backend/yard/lists";
            }
          })
        } else {
          layer.msg(res.data.msg)
        }
      })
    },
    delComponent: function (item) {
      var _index = this.componentList.indexOf(item);
      this.componentList.splice(_index, 1);

      this.resetOrder()//重置排序
    },
    changeIndexShow: function (item) {

      if (!item.indexShow) {
        this.$set(item, 'indexShow', true)
        return;
      }
      item.indexShow = !item.indexShow;
    },
    resetOrder:function(){
      var _this=this;
      setTimeout(function () {
       var componentList= document.querySelectorAll('.component-list')
        for(var i=0; i<componentList.length;i++){
         var time= componentList[i].getAttribute('time');
          _this.componentList.forEach(function (row) {
            if (row.time == time) {
              row.order = i;
            }
          })
        }
      }, 0)
    },
    initSwiper:function(){
      this.componentList.forEach(function(row){
        if(row.componentName=='banner'&&row.type==2&row.picList.length>1){
          setTimeout(function(){
            new Swiper('#swiper-banner', {
              loop: false,
              autoplay: {
                delay: parseInt(row.speed)*1000,
                disableOnInteraction: false,
              },
              preventClicks: false,
              pagination: {
                el: '.swiper-pagination',
                clickable: true,
              },
              onInit: function (swiper) {
              },
              onSlideChangeEnd: function (swiper) {
              }
            });
          },0)

        }
      })
    }
  },
  directives:{

  }
	}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

#left-defaults ::selection
{
	background-color:#fff
}
#right-defaults {
	/* display: flex;
	 flex-direction: column;*/
}
img{
	width: 100%;
}

.mt20 {
	margin-top: 20px;
}
.left-component.gu-mirror{
	background: #14C9CC;
	color: #fff;
	text-align: center;
	cursor: pointer;
	line-height: 35px;
}
.left-component.gu-transit{
   border:1px dashed #000;
	color: #000;
	text-align: center;
	cursor: pointer;
	line-height: 35px;
	margin-bottom: 15px;
}
.icon-show {
	display: inline-block;
	width: 15px;
	height: 16px;
	vertical-align: middle;
	cursor: pointer;
	background: url(/static/club/images/base.png) no-repeat scroll 5px -211px;
}

.icon-show-down {
	background: url(/static/club/images/base.png) no-repeat scroll 3px -231px;
}

.left-content.fixed{
	position: fixed;
	top: 0;
	width: 170px;
}
.left-content .title {
	height: 54px;
	text-indent: 15px;
	background: #eee;
	color: #333;
	margin: 0;
	padding: 0;
	line-height:54px;
	font-size: 16px;
}

.left-content #left-defaults {
	list-style: none;
}

.left-content #left-defaults > div {
	font-size: 14px;
	line-height: 40px;
	background: #fff;

	text-indent: 12px;
	cursor: pointer;
	list-style: none;
}

.left-content #left-defaults > div:active {

}

.left-content #left-defaults > div.t24 {
	text-indent: 24px;
}

.center-content .top_title {
	padding: 10px 0;
	background: #eee;
}

.component-list {
	border: 1px solid #eee;
	margin-bottom: 15px;
}

.component-list .head {
	padding: 8px 10px;
	font-size: 14px;
	cursor:pointer;
}

.component-list .component-content {
	padding: 20px;
}

.component-list .component-content .title {
	font-size: 14px;
	font-weight: bold;
	color: #333;
}

.component-body {
	border-top: 1px solid #eee;
}

.component-body .content {

}

.component-body .component-content .left-label {
	float: left;
	width: 65px;
	text-align: left;
}

.component-list .list-con {
	border: 1px solid #eee;
	margin-top: 10px;
	padding: 20px;
}

.component-list .list-con .items {
	border-bottom: 1px solid #eee;
	margin-bottom: 10px;
	position: relative;
}

.component-list .upload-con {
	width: 80px;
	height: 80px;
	background: #eee;
	background: url("/static/images/shangchuan@2x.png");
	background-size: contain;
	text-align: center;
	position: relative;
	overflow: hidden;
}

.upload-con input[type="file"] {
	width: 100%;
	height: 100%;
	opacity: 0;
	position: absolute;
	top: 0;
	bottom: 0;
	left: 0;
	right: 0;
	z-index: 100;
}

.component-list .upload-con span {
        position: absolute;
        bottom: 0px;
        font-size: 14px;
        text-align: center;
        display: block;
        width: 100%;
        height: 30px;
        line-height: 30px;
        color: #666;

}
</style>
