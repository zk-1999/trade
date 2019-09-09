<template>
    <div class="min1500">
      <el-breadcrumb separator-class="el-icon-arrow-right">
        <el-breadcrumb-item :to="{ path: '/' }">首页</el-breadcrumb-item>
        <el-breadcrumb-item>工作台</el-breadcrumb-item>
      </el-breadcrumb>
      <el-card class="gongzuo">
        <el-tabs :tab-position="tabPosition" style="height: 200px;">
        <el-tab-pane label="待我审批">待我审批</el-tab-pane>
        <el-tab-pane label="我已审批">我已审批</el-tab-pane>
        <el-tab-pane label="审批中">审批中</el-tab-pane>
        <el-tab-pane label="审批完成">审批完成</el-tab-pane>
        <el-tab-pane label="待出库">待出库</el-tab-pane>
        <el-tab-pane label="待入库">待入库</el-tab-pane>
      </el-tabs>
      </el-card>
      <el-card class="chaxun">
        <div class="cy">查询</div>
        <div class="tian">单据查询：
          <el-input placeholder="请输入查询单据" clearable  class="cor">
            <el-button slot="append" icon="el-icon-search"></el-button>
          </el-input>
        </div>
        <div class="tian">库存查询：
          <el-input placeholder="请输入查询库存" clearable  class="cor" >
            <el-button slot="append" icon="el-icon-search"></el-button>
          </el-input>
        </div>
        <div class="tian">客户查询：
          <el-input placeholder="请输入查询客户" clearable  class="cor" >
            <el-button slot="append" icon="el-icon-search"></el-button>
          </el-input>
        </div>
        <div class="tian">供应商查询：
          <el-input placeholder="请输入查询供应商" clearable  class="cor" >
            <el-button slot="append" icon="el-icon-search"></el-button>
          </el-input>
        </div>
      </el-card>
      <el-card class="yujing">
        <div class="cy">库存预警</div>
      </el-card>
     
    </div>
</template>
<script>
export default {
  data () {
    return {
    tabPosition: 'top',
    };
  },
    methods:{
    
    }
}
</script>
<style lang='less' scoped>
  .gongzuo{
    width: 70%;
    height: 660px;
    float: left;
    margin-right: 20px;
  }
  .chaxun{
    width: 28%;
    height: 340px;
  }
  .yujing{
    width: 28%;
    height: 300px;
  }
  .cy{
    width: 100%;
    height: 35px;
    border-bottom: 3px solid #eee;
  }
  .tian{
    text-align: right;

  }
  .cor{
    width: 260px;
    margin: 10px 0px;
    margin-left: 10px;
  }
</style>