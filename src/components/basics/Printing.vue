<template>
    <div class="min1500">
       <!-- 面包屑导航区域 -->
      <el-breadcrumb separator-class="el-icon-arrow-right">
        <el-breadcrumb-item :to="{ path: '/welcome' }">首页</el-breadcrumb-item>
        <el-breadcrumb-item>基础资料</el-breadcrumb-item>
        <el-breadcrumb-item>印刷参数</el-breadcrumb-item>
      </el-breadcrumb>
      <el-card>
        <el-row :gutter="20" class="row">
          <el-col :span="24">
             <el-row :gutter="20">
                <el-form :inline="true" class="demo-form-inline">
                    <el-form-item label="编号：">
                    <el-input placeholder="请输入编号"></el-input>
                    </el-form-item>
                    <el-form-item label="类型：">
                    <el-select placeholder="请选择类型">
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
            <el-table-column prop="a" label="型号"></el-table-column>
            <el-table-column prop="b" label="编号"></el-table-column>
            <el-table-column prop="c" label="单齿长/尺数" width="100px"></el-table-column>
            <el-table-column prop="d" label="齿数/尺数"></el-table-column>
            <el-table-column prop="e" label="纸宽/尺数"></el-table-column>
            <el-table-column prop="f" label="片数/尺数" ></el-table-column>
            <el-table-column prop="g" label="纸张/净门幅" width="100px"></el-table-column>
            <el-table-column prop="h" label="片数/净门幅" width="100px"></el-table-column>
            <el-table-column prop="i" label="可用纸长"></el-table-column>
            <el-table-column prop="j" label="计划纸长"></el-table-column>
            <el-table-column prop="k" label="放量"></el-table-column>
            <el-table-column prop="l" label="片数"></el-table-column>
            <el-table-column prop="m" label="印刷米数"></el-table-column>
            <el-table-column prop="n" label="印刷重量"></el-table-column>
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
        title="新增印刷参数"
        :visible.sync="addyonghuDialogVisible"
        width="50%"
        :before-close="handleClose">
        <el-form :label-position="labelPosition" label-width="120px">
            <el-row>
                <el-col :span="12">
                <el-form-item label="产品类型："><el-input placeholder="请输入产品类型"></el-input></el-form-item>
                <el-form-item label="产品型号："><el-input placeholder="请输入产品型号"></el-input></el-form-item>
                <el-form-item label="产品编号："><el-input placeholder="请输入产品编号"></el-input></el-form-item>
                <el-form-item label="单齿长/尺数："><el-input placeholder="单齿长/尺数"></el-input></el-form-item>
                <el-form-item label="齿数/尺数："><el-input placeholder="齿数/尺数"></el-input></el-form-item>          
                <el-form-item label="纸宽/尺数："><el-input placeholder="纸宽/尺数"></el-input></el-form-item>
                <el-form-item label="片数/尺数："><el-input placeholder="片数/尺数"></el-input></el-form-item>          
                <el-form-item label="纸张/净门幅："><el-input placeholder="纸张/净门幅"></el-input></el-form-item>
                <el-form-item label="片数/净门幅："><el-input placeholder="片数/净门幅"></el-input></el-form-item>
                </el-col>
                <el-col :span="12"> 
                <el-form-item label="可用纸长："><el-input placeholder="请输入可用纸长"></el-input></el-form-item>
                <el-form-item label="计划纸长："><el-input placeholder="请输入计划纸长"></el-input></el-form-item>
                <el-form-item label="放量："><el-input placeholder="请输入放量"></el-input></el-form-item>          
                <el-form-item label="片数："><el-input placeholder="请输入片数"></el-input></el-form-item>
                <el-form-item label="单个米数："><el-input placeholder="请输入单个米数"></el-input></el-form-item>
                <el-form-item label="单个重量："><el-input placeholder="请输入单个重量"></el-input></el-form-item>
                <el-form-item label="机台号："><el-input placeholder="请输入机台号"></el-input></el-form-item>
                <el-form-item label="模具号："><el-input placeholder="请输入模具号"></el-input></el-form-item>          
                <el-form-item label="产能："><el-input placeholder="请输入产能"></el-input></el-form-item>
                </el-col>
            </el-row>
        </el-form>
        <span slot="footer" class="dialog-footer">
          <el-button @click="addyonghuDialogVisible = false">取 消</el-button>
          <el-button type="primary" @click="addyonghuDialogVisible = false">确 定</el-button>
        </span>
      </el-dialog>
      <el-dialog
        title="编辑印刷参数"
        :visible.sync="edityonghuDialogVisible"
        width="48%"
        :before-close="handleClose">
       <el-form :label-position="labelPosition" label-width="120px">
            <el-row>
                <el-col :span="12">
                <el-form-item label="产品类型："><el-input placeholder="请输入产品类型" v-model="tableData[0].o"></el-input></el-form-item>
                <el-form-item label="产品型号："><el-input placeholder="请输入产品型号" v-model="tableData[0].a"></el-input></el-form-item>
                <el-form-item label="产品编号："><el-input placeholder="请输入产品编号" v-model="tableData[0].b"></el-input></el-form-item>
                <el-form-item label="单齿长/尺数："><el-input placeholder="单齿长/尺数" v-model="tableData[0].c"></el-input></el-form-item>
                <el-form-item label="齿数/尺数："><el-input placeholder="齿数/尺数" v-model="tableData[0].d"></el-input></el-form-item>          
                <el-form-item label="纸宽/尺数："><el-input placeholder="纸宽/尺数" v-model="tableData[0].e"></el-input></el-form-item>
                <el-form-item label="片数/尺数："><el-input placeholder="片数/尺数" v-model="tableData[0].f"></el-input></el-form-item>          
                <el-form-item label="纸张/净门幅："><el-input placeholder="纸张/净门幅" v-model="tableData[0].g"></el-input></el-form-item>
                <el-form-item label="片数/净门幅："><el-input placeholder="片数/净门幅" v-model="tableData[0].h"></el-input></el-form-item>
                </el-col>
                <el-col :span="12"> 
                <el-form-item label="可用纸长："><el-input placeholder="请输入可用纸长" v-model="tableData[0].i"></el-input></el-form-item>
                <el-form-item label="计划纸长："><el-input placeholder="请输入计划纸长" v-model="tableData[0].j"></el-input></el-form-item>
                <el-form-item label="放量："><el-input placeholder="请输入放量" v-model="tableData[0].k"></el-input></el-form-item>          
                <el-form-item label="片数："><el-input placeholder="请输入片数" v-model="tableData[0].l"></el-input></el-form-item>
                <el-form-item label="单个米数："><el-input placeholder="请输入单个米数" v-model="tableData[0].m"></el-input></el-form-item>
                <el-form-item label="单个重量："><el-input placeholder="请输入单个重量" v-model="tableData[0].n"></el-input></el-form-item>
                <el-form-item label="机台号："><el-input placeholder="请输入机台号"></el-input></el-form-item>
                <el-form-item label="模具号："><el-input placeholder="请输入模具号"></el-input></el-form-item>          
                <el-form-item label="产能："><el-input placeholder="请输入产能"></el-input></el-form-item>
                </el-col>
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
         tableData: [{
          a: '4oz单层',
          b: 'SW-04',
          c: '3.175',
          d:'125',
          e:'396.8750',
          f:'5',
          g:'732.7464',
          h:'4',
          i:'737',
          j:'737',
          k:'4.2536',
          l:'20',
          m:'586',
          n:'2667',
          o:'杯子'
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
      width: 230px;
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