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
                    <!-- <el-form-item label="类型：">
                    <el-select placeholder="请选择类型">
                      <el-option></el-option>
                    </el-select>
                    </el-form-item> -->
                    <el-form-item>
                        <el-button >查询</el-button>
                        <el-button type="primary">重置</el-button>
                    </el-form-item>
                </el-form>
        </el-row>
          <el-button type="success" @click="addyonghuDialogVisible = true">新增</el-button>
          <el-button
            type="warning"
            @click="selectedqi"
            :disabled="selectedList.length == 0"
          >批量启用/禁用</el-button>
          <el-button type="danger" @click="selected" :disabled="selectedList.length == 0">批量删除</el-button>
          <el-table border stripe :data="PrintingList" @selection-change="handleSelectionChange">
            <el-table-column type="selection" width="30"></el-table-column>
            <el-table-column type="index" width="30"></el-table-column>
            <el-table-column prop="parametersId" label="编号"></el-table-column>
            <el-table-column prop="parametersName" label="型号"></el-table-column>
            <el-table-column prop="productType" label="类型"></el-table-column>
            <el-table-column prop="parametersSingle" label="单齿长"></el-table-column>
            <el-table-column prop="parametersSinglenum" label="齿数"></el-table-column>
            <el-table-column prop="parametersPaperwidth" label="纸宽"  width="90px"></el-table-column>
            <el-table-column prop="parametersTeethnum" label="片数" ></el-table-column>
            <el-table-column prop="parametersDoorwidth" label="纸张"  width="90px"></el-table-column>
            <el-table-column prop="parametersDoornum" label="片数" ></el-table-column>
            <el-table-column prop="parametersUsablepaper" label="可用纸长"></el-table-column>
            <el-table-column prop="parametersPlanpaper" label="计划纸长"></el-table-column>
            <el-table-column prop="parametersVolume" label="放量"></el-table-column>
            <el-table-column prop="parametersNumber" label="片数"></el-table-column>
            <el-table-column prop="parametersMetre" label="印刷米数"></el-table-column>
            <el-table-column prop="parametersWeight" label="印刷重量"></el-table-column>
            <el-table-column prop="" label="机台号"></el-table-column>
            <el-table-column prop="" label="模具号"></el-table-column>
            <el-table-column prop="" label="产能"></el-table-column>
            <el-table-column label="状态" width="65px">
              <template>
                <el-switch active-color="#13ce66" inactive-color="#ff4949"></el-switch>
              </template>
            </el-table-column>
            <el-table-column label="操作" width="180px">
              <template>
                <el-button type="primary" icon="el-icon-edit" size="mini">修改</el-button>
                <el-button type="danger" icon="el-icon-delete" size="mini">删除</el-button>
              </template>
            </el-table-column>
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
      <!-- <el-dialog
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
                
            </el-row>
        </el-form>
        <span slot="footer" class="dialog-footer">
          <el-button @click="edityonghuDialogVisible = false">取 消</el-button>
          <el-button type="primary" @click="edityonghuDialogVisible = false">确 定</el-button>
        </span>
      </el-dialog> -->
      <el-dialog title="提示" :visible.sync="delVisible" width="300px">
      <div class="del-dialog-cnt">删除不可恢复，是否确定删除？</div>
      <span slot="footer" class="dialog-footer">
          <el-button @click="delVisible = false">取 消</el-button>
          <el-button type="primary" @click="deleteRow" >确 定</el-button>
      </span>
    </el-dialog>
    <el-dialog title="提示" :visible.sync="delVisibleqi" width="300px">
      <div class="del-dialog-cnt">此操作将批量启用, 是否继续？</div>
      <span slot="footer" class="dialog-footer">
          <el-button @click="delVisibleqi = false">取 消</el-button>
          <el-button type="primary" @click="deleteRowqi" >确 定</el-button>
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
      delVisible:false,
      delVisibleqi:false,
      currentPage1: 5,
      currentPage2: 5,
      currentPage3: 5,
      currentPage4: 4,
      selectedList: [],
      PrintingList:[],
      delarr:[],
      
    }
  },
  created () {
  },
  methods:{
    async getPrintingList() {
      const { data: res } = await this.$http.post("jc/Parameters/selectParameter");
      console.log(res);
      this.PrintingList = res;
    },
    selectedqi(){
      this.delarr=[];
      this.delVisibleqi = true;
      for (let i = 0; i < this.selectedList.length; i++) {
        this.delarr.push({supplierId:this.selectedList[i].supplierId,supState:this.selectedList[i].supState==1?0:1})
      }
      console.log(this.delarr);
    },
    selected(){
      this.delarr=[];
      this.delVisible = true;
      for (let i = 0; i < this.selectedList.length; i++) {
        this.delarr.push(this.selectedList[i].supplierId)
      }
      console.log(this.delarr);
    },
    async deleteRow(){
         const {data:res} = await this.$http.post('/jc/supplier/deleteSup',this.delarr);
         this.delVisible = false;
         this.getSupplierList();
      },
      async deleteRowqi(){
         const {data:res} = await this.$http.post('jc/supplier/updatestate',this.delarr);
         this.delVisibleqi = false;
         this.getSupplierList();
      },
    handleSelectionChange(val) {
      console.log(val);
      this.selectedList = val;
    },
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