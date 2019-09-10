<template>
    <div class="min1500">
       <!-- 面包屑导航区域 -->
      <el-breadcrumb separator-class="el-icon-arrow-right">
        <el-breadcrumb-item :to="{ path: '/welcome' }">首页</el-breadcrumb-item>
        <el-breadcrumb-item>基础资料</el-breadcrumb-item>
        <el-breadcrumb-item>生产商品类型</el-breadcrumb-item>
      </el-breadcrumb>
      <el-card>
        <el-row :gutter="20" class="row">
          <el-col :span="24">
             <el-row :gutter="20">
                <el-form :inline="true" class="demo-form-inline">
                    <el-form-item label="产品名称：">
                    <el-input placeholder="请输入产品名称"></el-input>
                    </el-form-item>
                    <el-form-item label="产品类型：">
                    <el-select placeholder="请选择产品类型">
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
          <el-table border stripe>
            <el-table-column type="selection" width="55"></el-table-column>
            <el-table-column type="index"></el-table-column>
            <el-table-column  label="产品编码"></el-table-column>
            <el-table-column  label="产品名称"></el-table-column>
            <el-table-column  label="产品类型"></el-table-column>
            <el-table-column  label="设计稿"></el-table-column>
            <el-table-column  label="纸张品牌/内" width="100px"></el-table-column>
            <el-table-column  label="克数"></el-table-column>
            <el-table-column  label="淋膜类型"></el-table-column>
            <el-table-column  label="纸张品牌/外" width="100px"></el-table-column>
            <el-table-column  label="克数"></el-table-column>
            <el-table-column  label="淋膜类型"></el-table-column>
            <el-table-column  label="纸张品牌/中" width="100px"></el-table-column>
            <el-table-column  label="克数"></el-table-column>
            <el-table-column  label="淋膜类型"></el-table-column>
            <el-table-column  label="状态"></el-table-column>
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
        title="新增生产商品"
        :visible.sync="addyonghuDialogVisible"
        width="50%"
        :before-close="handleClose">
        <el-form :label-position="labelPosition" label-width="120px">
            <el-row>
                <el-col :span="12">
                    <el-form-item label="产品编码："><el-input placeholder="请输入产品编码"></el-input></el-form-item>      <el-form-item label="产品名称："><el-input placeholder="请输入产品名称"></el-input></el-form-item>
                    <el-form-item label="产品类型："><el-input placeholder="请输入产品类型"></el-input></el-form-item>      <el-form-item label="设计稿："><el-input placeholder="请输入设计稿"></el-input></el-form-item>
                    <el-form-item label="纸张品牌/内："><el-input placeholder="请输入纸张品牌/内"></el-input></el-form-item>     <el-form-item label="克数/内："><el-input placeholder="请输入克数/内"></el-input></el-form-item>
                    <el-form-item label="淋膜类型/内："><el-input placeholder="请输入淋膜类型/内"></el-input></el-form-item>   
                </el-col>
                <el-col :span="12"> 
                    <el-form-item label="纸张品牌/外："><el-input placeholder="请输入纸张品牌/外"></el-input></el-form-item>     <el-form-item label="克数/外："><el-input placeholder="请输入克数/外"></el-input></el-form-item>
                    <el-form-item label="淋膜类型/外："><el-input placeholder="请输入淋膜类型/外"></el-input></el-form-item>  
                    <el-form-item label="纸张品牌/中："><el-input placeholder="请输入纸张品牌/中"></el-input></el-form-item>     <el-form-item label="克数/中："><el-input placeholder="请输入克数/中"></el-input></el-form-item>
                    <el-form-item label="淋膜类型/中："><el-input placeholder="请输入淋膜类型/中"></el-input></el-form-item>  
                    <el-form-item label="状态："><el-input placeholder="请输入状态"></el-input></el-form-item>
                </el-col>
            </el-row>
        </el-form>
        <span slot="footer" class="dialog-footer">
          <el-button @click="addyonghuDialogVisible = false">取 消</el-button>
          <el-button type="primary" @click="addyonghuDialogVisible = false">确 定</el-button>
        </span>
      </el-dialog>
      <el-dialog
        title="编辑生产商品"
        :visible.sync="edityonghuDialogVisible"
        width="48%"
        :before-close="handleClose">
       <el-form :label-position="labelPosition" label-width="120px">
            <el-row>
                <el-col :span="12">
                    <el-form-item label="产品编码："><el-input placeholder="请输入产品编码"></el-input></el-form-item>      <el-form-item label="产品名称："><el-input placeholder="请输入产品名称"></el-input></el-form-item>
                    <el-form-item label="产品类型："><el-input placeholder="请输入产品类型"></el-input></el-form-item>      <el-form-item label="设计稿："><el-input placeholder="请输入设计稿"></el-input></el-form-item>
                    <el-form-item label="纸张品牌/内："><el-input placeholder="请输入纸张品牌/内"></el-input></el-form-item>     <el-form-item label="克数/内："><el-input placeholder="请输入克数/内"></el-input></el-form-item>
                    <el-form-item label="淋膜类型/内："><el-input placeholder="请输入淋膜类型/内"></el-input></el-form-item>   
                </el-col>
                <el-col :span="12"> 
                    <el-form-item label="纸张品牌/外："><el-input placeholder="请输入纸张品牌/外"></el-input></el-form-item>     <el-form-item label="克数/外："><el-input placeholder="请输入克数/外"></el-input></el-form-item>
                    <el-form-item label="淋膜类型/外："><el-input placeholder="请输入淋膜类型/外"></el-input></el-form-item>  
                    <el-form-item label="纸张品牌/中："><el-input placeholder="请输入纸张品牌/中"></el-input></el-form-item>     <el-form-item label="克数/中："><el-input placeholder="请输入克数/中"></el-input></el-form-item>
                    <el-form-item label="淋膜类型/中："><el-input placeholder="请输入淋膜类型/中"></el-input></el-form-item>  
                    <el-form-item label="状态："><el-input placeholder="请输入状态"></el-input></el-form-item>
                </el-col>
            </el-row>
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