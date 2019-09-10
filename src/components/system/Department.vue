<template>
    <div class="min1500">
        <!-- 面包屑导航区域 -->
      <el-breadcrumb separator-class="el-icon-arrow-right">
        <el-breadcrumb-item :to="{ path: '/welcome' }">首页</el-breadcrumb-item>
        <el-breadcrumb-item>系统管理</el-breadcrumb-item>
        <el-breadcrumb-item>部门设置</el-breadcrumb-item>
      </el-breadcrumb>
      <el-card>
         <el-row :gutter="20">
           <span>&nbsp;&nbsp;&nbsp;部门名称：</span>
           <el-col :span="7">
            <el-input placeholder="请输入部门名称" clearable  class="cor" >
              <el-button slot="append" icon="el-icon-search"></el-button>
            </el-input>
           </el-col>
           <el-col :span="3">
            <el-button type="primary" class="chongzhi" >重置</el-button>
           </el-col>
        </el-row>
         <el-button type="success"  @click="addbumenDialogVisible = true">新增</el-button> <el-button type="warning" @click="editbumenDialogVisible= true">编辑</el-button> <el-button type="danger"  @click="deletebumen">删除</el-button>
          <el-table border stripe :data="tableData">
            <el-table-column type="selection" width="55"></el-table-column>
            <el-table-column type="index"></el-table-column>
            <!-- <el-table-column  label="部门编号"></el-table-column> -->
            <el-table-column prop="a" label="部门名称"></el-table-column>
            <el-table-column prop="b" label="备注"></el-table-column>
          </el-table>
      </el-card>
      <el-dialog
        title="新增部门"
        :visible.sync="addbumenDialogVisible"
        width="30%"
        :before-close="handleClose">
        <el-form :label-position="labelPosition" label-width="100px">
          <el-form-item label="部门名称："><el-input placeholder="请输入部门名称"></el-input></el-form-item>
          <el-form-item label="备注内容："><el-input type="textarea" :rows="2" placeholder="请输入备注内容"></el-input></el-form-item>
        </el-form>
        <span slot="footer" class="dialog-footer">
          <el-button @click="addbumenDialogVisible = false">取 消</el-button>
          <el-button type="primary" @click="addbumenDialogVisible = false">确 定</el-button>
        </span>
      </el-dialog>
      <el-dialog
        title="编辑部门"
        :visible.sync="editbumenDialogVisible"
        width="30%"
        :before-close="handleClose">
        <el-form :label-position="labelPosition" label-width="100px">
          <el-form-item label="部门名称："><el-input placeholder="请输入部门名称" v-model="tableData[0].a"></el-input></el-form-item>
          <el-form-item label="备注内容："><el-input type="textarea" :rows="2"  v-model="tableData[0].b" placeholder="请输入备注内容"></el-input></el-form-item>
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
      tableData: [{
          a: '惠普',
          b: '是',
          c: '原材料供应商',
          d:'祥子',
          e:'18859577302',
          f:'启用',
          g:'管理员',
          h:'2019-06-25 00:00',
          i:'53245454@qq.com',
          j:'',
          k:''
        }]
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
      this.$confirm('此操作将永久删除该部门, 是否继续?', '提示', {
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
    .el-button{
      margin-top: 15px;
    }
    .el-table{
      margin-top: 15px;
    }
    .chongzhi{
      margin-top: 0px;
    }
</style>