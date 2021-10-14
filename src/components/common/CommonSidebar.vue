<template>
  <aside class="main-sidebar">
    <!-- sidebar: style can be found in sidebar.less -->
    <section class="sidebar" style="height: auto; min-height: 100%;">
      <!-- sidebar menu: : style can be found in sidebar.less -->
      <ul class="sidebar-menu">

        <li class="treeview" :class="activenum == -1 ? 'active' : ''" @click="change(-1)">
          <a href="#/">
            <i class="fa fa-files-o"></i>
            <span>新建资源池</span>
          </a>
        </li>

        <!-- <li class="treeview" :class="activenum == -2 ? 'active' : ''" @click="change(-2)">
          <a href="#/pool">
            <i class="fa fa-files-o"></i>
            <span>资源池连接管理</span>
          </a>
        </li> -->

        <li class="treeview" :class="activenum == -6 ? 'active' : ''" @click="change(-6)">
          <a href="#/collect">
            <i class="fa fa-files-o"></i>
            <span>资源汇聚</span>
          </a>
        </li>

        <li v-for="(item,index) in items" :key="index" class="treeview" :class="activenum == index ? 'active' : ''" @click="change(index)">
          <a href="#/modeldetail">
            <i class="fa fa-files-o"></i>
            <span>{{item}}</span>
            <span class="pull-right-container">
              <small class="label pull-right bg-green">{{numbers[index]}}</small>
            </span>
          </a>
        </li>

        <li class="treeview" :class="activenum == -3 ? 'active' : ''" @click="change(-3)">
          <a href="#/company">
            <i class="fa fa-files-o"></i>
            <span>检验检测机构</span>
            <span class="pull-right-container">
              <small class="label pull-right bg-green">683</small>
            </span>
          </a>
        </li>

        <li class="treeview" :class="activenum == -4 ? 'active' : ''" @click="change(-4)">
          <a href="#/intelproperty">
            <i class="fa fa-files-o"></i>
            <span>知识产权机构</span>
            <span class="pull-right-container">
              <small class="label pull-right bg-green">158</small>
            </span>
          </a>
        </li>

        <!-- <li class="treeview" :class="activenum == -5 ? 'active' : ''" @click="change(-5)">
          <a href="#/expertgraph">
            <i class="fa fa-th"></i>
            <span>专家知识图谱</span>
          </a>
        </li> -->

        <!-- <li class="treeview" >
          <a href="http://10.108.210.65:10134" target="_blank">
            <i class="fa fa-th"></i>
            <span>仪器知识图谱</span>
            <span class="pull-right-container">
              <small class="label pull-right bg-green">10000+</small>
            </span>
          </a>
        </li>

        <li class="treeview" >
          <a href="http://10.108.210.65:10234" target="_blank">
            <i class="fa fa-pie-chart"></i>
            <span>专家知识图谱</span>
            <span class="pull-right-container">
              <small class="label pull-right bg-green">50000+</small>
            </span>
          </a>
        </li>

        <li class="treeview" >
          <a href="http://10.108.210.65:10434" target="_blank">
            <i class="fa fa-laptop"></i>
            <span>专利知识图谱</span>
            <span class="pull-right-container">
              <small class="label pull-right bg-green">100000+</small>
            </span>
          </a>
        </li> -->
      </ul>
    </section>
  </aside>

</template>

<script>
export default {
  name: "CommonSidebar",
  data() {
    return {
      numbers:[57095,25160,107081,0,0,0,0,0,0,0],
      items:[],
    };
  },
  mounted: function(){
    this.inits();
  },
  computed: {
    activenum: function(){
      return this.$store.state.page;
    }
  },
  methods:{
    change: function(index){
      if(this.$store.state.canUse<=0){
        // alert("尚未获得连接，请获取连接后使用");
      }
      var data = {
        type: index,
        title: this.$store.state.pagename[this.$store.state.page]
      };
      this.$http.post(`http://10.112.120.61:8000/ResourcePool/find_init`, data).then(
        response => {
          const { status, ok, body } = response;
          if (status === 200 && ok) {
            this.$store.state.result_name=body.name;
            this.$store.state.result_infor=body.infor;
          }
        },
        response => {
          console.log("error");
        }
      );
      this.$store.state.page=index;
    },
    inits: function(){
      this.$http.post(`http://10.112.120.61:8000/ResourcePool/take_tables`).then(
        response => {
          const { status, ok, body } = response;
          if (status === 200 && ok) {
            this.items=body;
            this.$store.state.pagename=body;
          }
        },
        response => {
          console.log("error");
        }
      );
    }
  }
};
</script>

