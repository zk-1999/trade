<template>
    <div>
        <!-- 面包屑导航区域 -->
      <el-breadcrumb separator-class="el-icon-arrow-right">
        <el-breadcrumb-item :to="{ path: '/welcome' }">首页</el-breadcrumb-item>
        <el-breadcrumb-item>系统管理</el-breadcrumb-item>
        <el-breadcrumb-item>菜单管理</el-breadcrumb-item>
      </el-breadcrumb>
      <el-card>
         <el-row :gutter="20">
           <span>&nbsp;&nbsp;&nbsp;菜单名称：</span>
           <el-col :span="7">
            <el-input placeholder="请输入菜单名称" clearable  class="cor" >
              <el-button slot="append" icon="el-icon-search"></el-button>
            </el-input>
           </el-col>
           <el-col :span="3">
            <el-button type="primary">重置</el-button>
           </el-col>
        </el-row>
         <el-button type="success" @click="addbumenDialogVisible = true">新增</el-button>
         <el-button type="warning" @click="editbumenDialogVisible= true">编辑</el-button>
         <el-button type="danger" @click="deletebumen">删除</el-button>
          <el-table border stripe>
            <el-table-column type="index"></el-table-column>
            <el-table-column prop="roleName" label="一级菜单名称"></el-table-column>
            <el-table-column prop="roleDesc" label="二级菜单名称"></el-table-column>
            <el-table-column width="290px" label="菜单访问路径"></el-table-column>
          </el-table>
      </el-card>
      <el-dialog
        title="新增菜单"
        :visible.sync="addbumenDialogVisible"
        width="30%"
        :before-close="handleClose">
        <el-form :label-position="labelPosition" label-width="120px">
          <el-form-item label="一级菜单名称："><el-input placeholder="请输入一级菜单名称"></el-input></el-form-item>
          <el-form-item label="二级菜单名称："><el-input placeholder="请输入二级菜单名称"></el-input></el-form-item>
          <el-form-item label="菜单访问路径："><el-input placeholder="请输入菜单访问路径"></el-input></el-form-item>
        </el-form>
        <span slot="footer" class="dialog-footer">
          <el-button @click="addbumenDialogVisible = false">取 消</el-button>
          <el-button type="primary" @click="addbumenDialogVisible = false">确 定</el-button>
        </span>
      </el-dialog>
      <el-dialog
        title="编辑菜单"
        :visible.sync="editbumenDialogVisible"
        width="30%"
        :before-close="handleClose">
        <el-form :label-position="labelPosition" label-width="120px">
          <el-form-item label="一级菜单名称："><el-input placeholder="请输入一级菜单名称"></el-input></el-form-item>
          <el-form-item label="二级菜单名称："><el-input placeholder="请输入二级菜单名称"></el-input></el-form-item>
          <el-form-item label="菜单访问路径："><el-input placeholder="请输入菜单访问路径"></el-input></el-form-item>
        </el-form>
        <span slot="footer" class="dialog-footer">
          <el-button @click="editbumenDialogVisible = false">取 消</el-button>
          <el-button type="primary" @click="editbumenDialogVisible = false">确 定</el-button>
        </span>
      </el-dialog>


    </div>
</template>
<script>
export default {
  data () {
    return {
      labelPosition: 'right',
      addbumenDialogVisible: false,
      editbumenDialogVisible:false,
    }
  },
  created () {
  },
  methods:{
    handleClose(done) {
        this.$confirm('确认关闭？')
          .then(_ => {
            done();
          })
          .catch(_ => {});
    },
    deletebumen(){
      this.$confirm('此操作将永久删除该菜单, 是否继续?', '提示', {
          confirmButtonText: '确定',
          cancelButtonText: '取消',
          type: 'warning'
        }).then(() => {
          this.$message({
            type: 'success',
            message: '删除成功!'
          });
        }).catch(() => {
          this.$message({
            type: 'info',
            message: '已取消删除'
          });          
        });
      
    }
  }
}
</script>
<style lang='less' scoped>
    .el-card{
        margin-top: 15px;
    }
    .el-row{
        align-items: center;
        display: flex;
    }
    .el-table{
        margin-top: 15px;
    }
    .el-button{
      margin-top: 15px;
    }
</style>