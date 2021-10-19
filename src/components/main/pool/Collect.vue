<template>
<div class="content-wrapper" style="min-height:960px;">
  <section class="content">
    <div class="row">
      <div class="col-xs-6">
        <div class="box">
          <div class="box-header">
            <div class="form-group">
            <label>选择第三方平台</label>
            <select class="form-control" v-model="choose1">
              <option v-for="(platform,index) in platforms" :key="index">{{platform}}</option>
            </select>
          </div>
            <button class="btn btn-success pull-right" data-toggle="modal" @click="changePlatform1">确认</button>
            <h3 class="box-title">{{platform1}} <b>{{ratio1}}</b></h3>
          </div>
          <div class="box-body table-responsive">
            <table class="table table-bordered table-striped" style="table-layout:fixed;">
              <tbody>
                <tr>
                  <td v-for="(title,index) in titles1" :key="index">{{title}}</td>
                </tr>
                <tr v-for="(item,index) in items1" :key="index">
                  <td v-for="(column,index) in item" :key="index">{{column}}</td>
                </tr>
              </tbody>
            </table>
          </div>
          <common-alert :show="show" :error="error" :info="info"></common-alert>
        </div>
      </div>

      <div class="col-xs-6">
        <div class="box">
          <div class="box-header">
            <div class="form-group">
            <label>选择第三方平台</label>
            <select class="form-control" v-model="choose2">
              <option v-for="(platform,index) in platforms" :key="index">{{platform}}</option>
            </select>
          </div>
            <button class="btn btn-success pull-right" data-toggle="modal" @click="changePlatform2">确认</button>
            <h3 class="box-title">{{platform2}} <b>{{ratio2}}</b></h3>
          </div>
          <div class="box-body table-responsive">
            <table class="table table-bordered table-striped" style="table-layout:fixed;">
              <tbody>
                <tr>
                  <td v-for="(title,index) in titles2" :key="index">{{title}}</td>
                </tr>
                <tr v-for="(item,index) in items2" :key="index">
                  <td v-for="(column,index) in item" :key="index">{{column}}</td>
                </tr>
              </tbody>
            </table>
          </div>
          <common-alert :show="show" :error="error" :info="info"></common-alert>
        </div>
      </div>
    </div>

    <div class="row">
      <div class="col-xs-12">
        <div class="box">
          <div class="box-header">
            <button class="btn btn-success pull-right" data-toggle="modal" @click="abc">汇聚</button>
            <h3 class="box-title">{{platform3}} <b>{{ratio3}}</b></h3>
          </div>
          <div class="box-body table-responsive">
            <table class="table table-bordered table-striped" style="table-layout:fixed;">
              <tbody>
                <tr>
                  <td v-for="(title,index) in titles3" :key="index">{{title}}</td>
                </tr>
                <tr v-for="(item,index) in items3" :key="index">
                  <td v-for="(column,index) in item" :key="index">{{column}}</td>
                </tr>
              </tbody>
            </table>
          </div>
          <common-alert :show="show" :error="error" :info="info"></common-alert>
        </div>
      </div>
    </div>

    <div class="row">
      <div class="col-xs-12">
        <div class="box">
          <div class="box-header">
            <h3 class="box-title">字段对应关系 </h3>
          </div>
          <div class="box-body table-responsive">
            <table class="table table-bordered table-striped" style="table-layout:fixed;">
              <tbody>
                <tr>
                  <td v-for="(title,index) in titles4" :key="index">{{title}}</td>
                </tr>
                <tr v-for="(item,index) in items4" :key="index">
                  <td v-for="(column,index) in item" :key="index">{{column}}</td>
                </tr>
              </tbody>
            </table>
          </div>
          <common-alert :show="show" :error="error" :info="info"></common-alert>
        </div>
      </div>
    </div>

  </section>
</div>
</template>
<script>
import { format, getPath } from "../../../util/index";
import CommonAlert from "@/components/common/CommonAlert";

export default {
  name: "Collect",
  components: {
    CommonAlert
  },
  data() {
    return {
      choose1:"",
      choose2:"",
      platforms:["好专家网","重庆科技服务平台","黑龙江科技服务平台","哈长城市群科技服务平台"],
      ratio1:"",
      ratio2:"",
      ratio3:"",
      platform1:"",
      platform2:"",
      platform3:"",
      titles1:[],
      items1: [],
      titles2:[],
      items2: [],
      titles3:[],
      items3: [],
      titles4:[],
      items4: [],
      items31: [],
      titles41:[],
      items41: [],
      info: "",
      show: false,
      error: false
    };
  },
  mounted() {
    this.init();
  },
  methods: {
    init: function() {
      this.$http.post(`http://localhost:8000/ResourcePool/init`).then(
        response => {
          const { status, ok, body } = response;
          if (status === 200 && ok) {
            this.ratio1=body.ratio1;
            this.ratio2=body.ratio2;
            this.ratio3=body.ratio3;
            this.platform1=body.platform1;
            this.platform2=body.platform2;
            this.platform3=body.platform3;
            this.titles1=body.titles1;
            this.items1=body.items1;
            this.titles2=body.titles2;
            this.items2=body.items2;
            this.titles3=body.titles3;
            this.items31=body.items3;
            this.titles41=body.titles4;
            this.items41=body.items4;
          }
        },
        response => {
          console.log("error");
        }
      );
    },
    changePlatform1: function(){
      var data = {
        choose1: this.choose1,
        choose2: this.platform2
      };
      this.$http.post(`http://localhost:8000/ResourcePool/changePlatform`,data).then(
        response => {
          const { status, ok, body } = response;
          if (status === 200 && ok) {
            this.ratio1=body.ratio1;
            this.ratio2=body.ratio2;
            this.ratio3=body.ratio3;
            this.platform1=body.platform1;
            this.platform2=body.platform2;
            this.platform3=body.platform3;
            this.titles1=body.titles1;
            this.items1=body.items1;
            this.titles2=body.titles2;
            this.items2=body.items2;
            this.titles3=body.titles3;
            this.items31=body.items3;
            this.titles41=body.titles4;
            this.items41=body.items4;
            this.items3=[];
            this.titles4=[];
            this.items4=[];
          }
        },
        response => {
          console.log("error");
        }
      );
    },
    changePlatform2: function(){
      var data = {
        choose1: this.platform1,
        choose2: this.choose2
      };
      this.$http.post(`http://localhost:8000/ResourcePool/changePlatform`,data).then(
        response => {
          const { status, ok, body } = response;
          if (status === 200 && ok) {
            this.ratio1=body.ratio1;
            this.ratio2=body.ratio2;
            this.ratio3=body.ratio3;
            this.platform1=body.platform1;
            this.platform2=body.platform2;
            this.platform3=body.platform3;
            this.titles1=body.titles1;
            this.items1=body.items1;
            this.titles2=body.titles2;
            this.items2=body.items2;
            this.titles3=body.titles3;
            this.items31=body.items3;
            this.titles41=body.titles4;
            this.items41=body.items4;
            this.items3=[];
            this.titles4=[];
            this.items4=[];
          }
        },
        response => {
          console.log("error");
        }
      );
    },
    abc: function(){
      this.items3=this.items31;
      this.titles4=this.titles41;
      this.items4=this.items41;
    }
  }
};
</script>
<style scoped>
</style>
