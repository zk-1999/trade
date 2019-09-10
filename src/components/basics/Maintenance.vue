<template>
    <div class="min1500">
       <!-- 面包屑导航区域 -->
      <el-breadcrumb separator-class="el-icon-arrow-right">
        <el-breadcrumb-item :to="{ path: '/welcome' }">首页</el-breadcrumb-item>
        <el-breadcrumb-item>基础资料</el-breadcrumb-item>
        <el-breadcrumb-item>基础数据维护</el-breadcrumb-item>
      </el-breadcrumb>
      <el-card>
        <el-row :gutter="20" class="row">
          <el-col :span="24">
             <el-row :gutter="20">
                <el-form :inline="true" class="demo-form-inline">
                    <el-form-item label="产品编号：">
                        <el-select placeholder="请选择产品编号">
                        <el-option></el-option>
                        </el-select>
                    </el-form-item>
                    <el-form-item label="产品名称：">
                        <el-select placeholder="请选择产品名称">
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
          <div class="fenge"></div>
          <el-tabs :tab-position="tabPosition" style="height: 450px;" type="border-card">
            <el-tab-pane label="产品编号名称">
              <el-table border stripe>
                <el-table-column type="selection" width="55"></el-table-column>
                <el-table-column type="index"></el-table-column>
                <el-table-column  label="名称"></el-table-column>
                <el-table-column  label="所属基础数据"></el-table-column>
                <el-table-column  label="状态"></el-table-column>
              </el-table>
            </el-tab-pane>
            <el-tab-pane label="纸张品牌">
              <el-table border stripe>
                <el-table-column type="selection" width="55"></el-table-column>
                <el-table-column type="index"></el-table-column>
                <el-table-column  label="名称"></el-table-column>
                <el-table-column  label="所属基础数据"></el-table-column>
                <el-table-column  label="状态"></el-table-column>
              </el-table>
            </el-tab-pane>
            <el-tab-pane label="淋膜类型">
              <el-table border stripe>
                <el-table-column type="selection" width="55"></el-table-column>
                <el-table-column type="index"></el-table-column>
                <el-table-column label="名称"></el-table-column>
                <el-table-column label="所属基础数据"></el-table-column>
                <el-table-column label="状态"></el-table-column>
              </el-table>
            </el-tab-pane>
            <el-tab-pane label="纸张克重">
              <el-table border stripe>
                <el-table-column type="selection" width="55"></el-table-column>
                <el-table-column type="index"></el-table-column>
                <el-table-column label="名称"></el-table-column>
                <el-table-column label="所属基础数据"></el-table-column>
                <el-table-column label="状态"></el-table-column>
              </el-table>
            </el-tab-pane>
            <el-tab-pane label="配盖">
              <el-table border stripe>
                <el-table-column type="selection" width="55"></el-table-column>
                <el-table-column type="index"></el-table-column>
                <el-table-column label="名称"></el-table-column>
                <el-table-column label="所属基础数据"></el-table-column>
                <el-table-column label="状态"></el-table-column>
              </el-table>
            </el-tab-pane>
            <el-tab-pane label="印刷方式">
              <el-table border stripe>
                <el-table-column type="selection" width="55"></el-table-column>
                <el-table-column type="index"></el-table-column>
                <el-table-column label="名称"></el-table-column>
                <el-table-column label="所属基础数据"></el-table-column>
                <el-table-column label="状态"></el-table-column>
              </el-table>
            </el-tab-pane>
            <el-tab-pane label="库存单位">
              <el-table border stripe>
                <el-table-column type="selection" width="55"></el-table-column>
                <el-table-column type="index"></el-table-column>
                <el-table-column label="名称"></el-table-column>
                <el-table-column label="所属基础数据"></el-table-column>
                <el-table-column label="状态"></el-table-column>
              </el-table>
            </el-tab-pane>
            <el-tab-pane label="供应商类型">
              <el-table border stripe>
                <el-table-column type="selection" width="55"></el-table-column>
                <el-table-column type="index"></el-table-column>
                <el-table-column label="名称"></el-table-column>
                <el-table-column label="所属基础数据"></el-table-column>
                <el-table-column label="状态"></el-table-column>
              </el-table>
            </el-tab-pane>
            <el-tab-pane label="包装类型1">
              <el-table border stripe>
                <el-table-column type="selection" width="55"></el-table-column>
                <el-table-column type="index"></el-table-column>
                <el-table-column label="名称"></el-table-column>
                <el-table-column label="所属基础数据"></el-table-column>
                <el-table-column label="状态"></el-table-column>
              </el-table>
            </el-tab-pane>
            <el-tab-pane label="包装类型2">
              <el-table border stripe>
                <el-table-column type="selection" width="55"></el-table-column>
                <el-table-column type="index"></el-table-column>
                <el-table-column label="名称"></el-table-column>
                <el-table-column label="所属基础数据"></el-table-column>
                <el-table-column label="状态"></el-table-column>
              </el-table>
            </el-tab-pane>
            <el-tab-pane label="货币类型">
              <el-table border stripe>
                <el-table-column type="selection" width="55"></el-table-column>
                <el-table-column type="index"></el-table-column>
                <el-table-column label="名称"></el-table-column>
                <el-table-column label="所属基础数据"></el-table-column>
                <el-table-column label="状态"></el-table-column>
              </el-table>
            </el-tab-pane>
            <el-tab-pane label="收入类型">
              <el-table border stripe>
                <el-table-column type="selection" width="55"></el-table-column>
                <el-table-column type="index"></el-table-column>
                <el-table-column label="名称"></el-table-column>
                <el-table-column label="所属基础数据"></el-table-column>
                <el-table-column label="状态"></el-table-column>
              </el-table>
            </el-tab-pane>
            <el-tab-pane label="支出类型">
              <el-table border stripe>
                <el-table-column type="selection" width="55"></el-table-column>
                <el-table-column type="index"></el-table-column>
                <el-table-column label="名称"></el-table-column>
                <el-table-column label="所属基础数据"></el-table-column>
                <el-table-column label="状态"></el-table-column>
              </el-table>
            </el-tab-pane>
            <el-tab-pane label="产品刀模">
              <el-table border stripe>
                <el-table-column type="selection" width="55"></el-table-column>
                <el-table-column type="index"></el-table-column>
                <el-table-column label="名称"></el-table-column>
                <el-table-column label="所属基础数据"></el-table-column>
                <el-table-column label="状态"></el-table-column>
              </el-table>
            </el-tab-pane>
            <el-tab-pane label="仓库类型">
              <el-table border stripe>
                <el-table-column type="selection" width="55"></el-table-column>
                <el-table-column type="index"></el-table-column>
                <el-table-column label="名称"></el-table-column>
                <el-table-column label="所属基础数据"></el-table-column>
                <el-table-column label="状态"></el-table-column>
              </el-table>
            </el-tab-pane>
          </el-tabs>
          </el-col>
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
        title="新增基础数据"
        :visible.sync="addyonghuDialogVisible"
        width="30%"
        :before-close="handleClose">
        <el-form :label-position="labelPosition" label-width="120px">
            <el-form-item label="名称："><el-input placeholder="请输入名称"></el-input></el-form-item>
            <el-form-item label="所属基础数据："><el-input placeholder="请输入所属基础数据"></el-input></el-form-item>
            <el-form-item label="状态："><el-input placeholder="请输入状态"></el-input></el-form-item>
        </el-form>
        <span slot="footer" class="dialog-footer">
          <el-button @click="addyonghuDialogVisible = false">取 消</el-button>
          <el-button type="primary" @click="addyonghuDialogVisible = false">确 定</el-button>
        </span>
      </el-dialog>
      <el-dialog
        title="编辑基础数据"
        :visible.sync="edityonghuDialogVisible"
        width="30%"
        :before-close="handleClose">
        <el-form :label-position="labelPosition" label-width="120px">
          <el-form-item label="名称："><el-input placeholder="请输入名称"></el-input></el-form-item>
          <el-form-item label="所属基础数据"><el-input placeholder="请输入所属基础数据"></el-input></el-form-item>
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
        tabPosition: 'left',
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
      width: 225px;
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
    .fenge{
        width: 100%;
        height: 20px;
        background: #eee;
        margin-top: 15px;
    }
    .el-card{
        height: 680px;
    }
    .el-pagination{
        // text-align: right;
        // margin-right: 50px;
        margin-top: 10px;
    }
</style>