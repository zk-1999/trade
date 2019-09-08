<template>
    <div>
        <!-- 面包屑导航区域 -->
      <el-breadcrumb separator-class="el-icon-arrow-right">
        <el-breadcrumb-item :to="{ path: '/welcome' }">首页</el-breadcrumb-item>
        <el-breadcrumb-item>系统管理</el-breadcrumb-item>
        <el-breadcrumb-item>系统日志</el-breadcrumb-item>
      </el-breadcrumb>
      <el-card>
        <el-button type="primary">导出日志</el-button>
        <el-table border stripe>
          <el-table-column type="index"></el-table-column>
          <el-table-column prop="roleName" label="时间"></el-table-column>
          <el-table-column prop="roleDesc" label="用户"></el-table-column>
          <el-table-column width="290px" label="所属部门"></el-table-column>
          <el-table-column prop="roleName" label="所属职位"></el-table-column>
          <el-table-column prop="roleDesc" label="IP地址"></el-table-column>
          <el-table-column width="290px" label="操作记录"></el-table-column>
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
        currentPage4: 4
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
    .el-table{
      margin-top: 15px;
    }
    .el-button{
      float: right;
    }
    .el-pagination{
      margin-top: 30px;
    }
</style>