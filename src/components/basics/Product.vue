<template>
    <div class="min1500">
       <!-- 面包屑导航区域 -->
      <el-breadcrumb separator-class="el-icon-arrow-right">
        <el-breadcrumb-item :to="{ path: '/welcome' }">首页</el-breadcrumb-item>
        <el-breadcrumb-item>基础资料</el-breadcrumb-item>
        <el-breadcrumb-item>产品设计稿维护</el-breadcrumb-item>
      </el-breadcrumb>
      <el-card>
        <el-row :gutter="20" class="row">
          <el-col :span="24">
             <el-row :gutter="20">
                <el-form :inline="true" class="demo-form-inline">
                    <el-form-item label="设计稿编码：">
                    <el-input placeholder="请输入名称"></el-input>
                    </el-form-item>
                    <el-form-item label="颜色：">
                    <el-input placeholder="请输入颜色"></el-input>
                    </el-form-item>
                    <el-form-item label="状态：">
                    <el-select placeholder="请选择状态">
                      <el-option></el-option>
                    </el-select>
                    </el-form-item>
                    <el-form-item>
                        <el-button >查询</el-button>
                        <el-button type="primary">重置</el-button>
                    </el-form-item>
                </el-form>
        </el-row>
          <el-button type="success" @click="addyonghuDialogVisible = true">新增</el-button>
          <el-button type="warning" @click="edityonghuDialogVisible= true">编辑</el-button>
          <el-button type="danger" @click="deletebumen">删除</el-button>
          <el-button type="info" @click="deletebumen">启用、禁用</el-button>
          <el-table border stripe :data="tableData">
            <el-table-column type="selection" width="55"></el-table-column>
            <el-table-column type="index"></el-table-column>
            <el-table-column prop="a" label="设计稿编码"></el-table-column>
            <!-- <el-table-column prop="b" label="名称"></el-table-column> -->
            <el-table-column prop="b" label="颜色"></el-table-column>
            <el-table-column prop="" label="图片"></el-table-column>
            <el-table-column prop="" label="状态"></el-table-column>
          </el-table></el-col>
        </el-row>
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
      <el-dialog
        title="新增产品设计稿"
        :visible.sync="addyonghuDialogVisible"
        width="40%"
        :before-close="handleClose">
        <el-form :label-position="labelPosition" label-width="120px">
            <el-form-item label="产品型号："><el-input placeholder="请输入产品型号"></el-input></el-form-item>      <el-form-item label="产品日期："><el-input placeholder="请输入产品日期"></el-input></el-form-item>
            <el-form-item label="产品名称："><el-input placeholder="请输入产品名称"></el-input></el-form-item>      <el-form-item label="颜色：">
              <el-row>
                <el-col :span="12">
                   <el-input placeholder="请输入颜色1"></el-input>
                   <el-input placeholder="请输入颜色2"></el-input>
                   <el-input placeholder="请输入颜色3"></el-input>
                   <el-input placeholder="请输入颜色4"></el-input>
                </el-col>
                 <el-col :span="12">
                   <el-input placeholder="请输入颜色5"></el-input>
                   <el-input placeholder="请输入颜色6"></el-input>
                   <el-input placeholder="请输入颜色7"></el-input>
                   <el-input placeholder="请输入颜色8"></el-input>
                </el-col>
               </el-row>
            </el-form-item>
            <el-form-item label="上传设计稿：">
                <el-image >
                    <div slot="placeholder" class="image-slot">
                       <img src="../../assets/logo.png" alt="">
                    </div>
                </el-image>
            </el-form-item>
            <el-form-item label="状态："><el-input placeholder="请输入状态"></el-input></el-form-item>  
        </el-form>
        <span slot="footer" class="dialog-footer">
          <el-button @click="addyonghuDialogVisible = false">取 消</el-button>
          <el-button type="primary" @click="addyonghuDialogVisible = false">确 定</el-button>
        </span>
      </el-dialog>
      <el-dialog
        title="编辑产品设计稿"
        :visible.sync="edityonghuDialogVisible"
        width="40%"
        :before-close="handleClose">
        <el-form :label-position="labelPosition" label-width="120px">
            <el-form-item label="产品型号："><el-input placeholder="请输入产品型号" v-model="tableData[0].d"></el-input></el-form-item>      <el-form-item label="产品日期："><el-input placeholder="请输入产品日期" v-model="tableData[0].e"></el-input></el-form-item>
            <el-form-item label="产品名称："><el-input placeholder="请输入产品名称" v-model="tableData[0].f"></el-input></el-form-item>      <el-form-item label="颜色：">
              <el-row>
                <el-col :span="12">
                   <el-input placeholder="请输入颜色1" v-model="tableData[0].b"></el-input>
                   <el-input placeholder="请输入颜色2"></el-input>
                   <el-input placeholder="请输入颜色3"></el-input>
                   <el-input placeholder="请输入颜色4"></el-input>
                </el-col>
                 <el-col :span="12">
                   <el-input placeholder="请输入颜色5"></el-input>
                   <el-input placeholder="请输入颜色6"></el-input>
                   <el-input placeholder="请输入颜色7"></el-input>
                   <el-input placeholder="请输入颜色8"></el-input>
                </el-col>
               </el-row>
            </el-form-item>
            <el-form-item label="上传设计稿：">
                <el-image >
                    <div slot="placeholder" class="image-slot">
                       <!-- <img src="../../assets/logo.png" alt=""> -->
                    </div>
                </el-image>
            </el-form-item>
            <el-form-item label="状态："><el-input placeholder="请输入状态"></el-input></el-form-item>  
        </el-form>
        <span slot="footer" class="dialog-footer">
          <el-button @click="edityonghuDialogVisible = false">取 消</el-button>
          <el-button type="primary" @click="edityonghuDialogVisible = false">确 定</el-button>
        </span>
      </el-dialog>
    </div>
</template>
<script>
export default {
  data () {
    return {
        labelPosition: 'right',
        addyonghuDialogVisible: false,
        edityonghuDialogVisible:false,
        resetPassdialogVisible:false,
        currentPage1: 5,
        currentPage2: 5,
        currentPage3: 5,
        currentPage4: 4,
           tableData: [{
          a: '8SW-20190510-Hansson Hammar',
          b: 'red',
          c: '原材料供应商',
          d:'8SW',
          e:'20190510',
          f:'Hansson Hammar',
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
     handleSizeChange(val) {
      console.log(`每页 ${val} 条`);
    },
    handleCurrentChange(val) {
      console.log(`当前页: ${val}`);
    },
    handleClose(done) {
        this.$confirm('确认关闭？')
          .then(_ => {
            done();
          })
          .catch(_ => {});
    },
    deletebumen(){
      this.$confirm('此操作将永久删除该职务, 是否继续?', '提示', {
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
    },
     handleNodeClick(data) {
        console.log(data);
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
    .demo-form-inline .el-input{
      width: 170px;
    }
    .el-select{
      width: 265px;
    }
    .xiang{
      width: 400px;
    }
    .hu{
      width: 133px;
    }
   .el-col{
        .el-input{
            width: 200px;
        }
        .el-form-item{
          .el-select{
            width: 200px;
          }
        }
    }
</style>