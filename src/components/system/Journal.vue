<template>
    <div class="min1500">
        <!-- 面包屑导航区域 -->
      <el-breadcrumb separator-class="el-icon-arrow-right">
        <el-breadcrumb-item :to="{ path: '/welcome' }">首页</el-breadcrumb-item>
        <el-breadcrumb-item>系统管理</el-breadcrumb-item>
        <el-breadcrumb-item>系统日志</el-breadcrumb-item>
      </el-breadcrumb>
      <el-card>
        <el-button type="primary">导出日志</el-button>
        <el-table border stripe :data="table">
          <el-table-column type="selection" width="55"></el-table-column>
          <el-table-column type="index"></el-table-column>
          <el-table-column prop="a" label="时间"></el-table-column>
          <el-table-column prop="b" label="用户"></el-table-column>
          <el-table-column prop="c" label="所属部门"></el-table-column>
          <el-table-column prop="d" label="所属职位"></el-table-column>
          <el-table-column prop="e" label="IP地址"></el-table-column>
          <el-table-column prop="f" label="操作记录"></el-table-column>
        </el-table>
        <el-pagination
          @size-change="handleSizeChange"
          @current-change="handleCurrentChange"
          :current-page="currentPage4"
          :page-sizes="[100, 200, 300, 400]"
          :page-size="100"
          layout="total, sizes, prev, pager, next, jumper"
          :total="400">
        </el-pagination>
      </el-card>
    </div>
</template> 
<script>
export default {
  data () {
    return {
        currentPage1: 5,
        currentPage2: 5,
        currentPage3: 5,
        currentPage4: 4,
        table: [{
          a: '2019-09-03 14:36:21',
          b: 'admin',
          c: '采购部门',
          d:'主管',
          e:'189.12.135.21',
          f:'登录',
        }],
    }
  },
  created () {
  },
  methods:{
    handleSizeChange(val) {
    console.log(`每页 ${val} 条`);
    },
    handleCurrentChange(val) {
    console.log(`当前页: ${val}`);
    }
  }
}
</script>
<style lang='less' scoped>
    .el-card{
      margin-top: 15px;
    }
 
    .el-button{
      float: right;
      margin-bottom: 15px;
    }
    .el-pagination{
      margin-top: 30px;
    }
</style>