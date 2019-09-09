<template>
    <div class="min1500">
       <!-- 面包屑导航区域 -->
      <el-breadcrumb separator-class="el-icon-arrow-right">
        <el-breadcrumb-item :to="{ path: '/welcome' }">首页</el-breadcrumb-item>
        <el-breadcrumb-item>基础资料</el-breadcrumb-item>
        <el-breadcrumb-item>供应商商品管理</el-breadcrumb-item>
      </el-breadcrumb>
      <el-card class="quan">
        <div class="shu">
          <div class="togglr-button">全部部门</div>  
          <el-button type="text">供应商名称1</el-button>
          <el-button type="text">供应商名称2</el-button>
          <el-button type="text">供应商名称3</el-button>
          <el-button type="text">供应商名称4</el-button>
          <el-button type="text">供应商名称5</el-button>
          <el-button type="text">供应商名称6</el-button>
          <el-button type="text">供应商名称7</el-button>
          <el-button type="text">供应商名称8</el-button>
          <el-button type="text">供应商名称9</el-button>
        </div>
      </el-card>
      <el-card>
        <el-row :gutter="20" class="row">
          <el-col :span="24">
            <el-row :gutter="20">
                <span>&nbsp;&nbsp;&nbsp;职务名称：</span>
                <el-col :span="7">
                  <el-input placeholder="请输入职务名称" clearable  class="cor">
                    <el-button slot="append" icon="el-icon-search"></el-button>
                  </el-input>
                </el-col>
                <el-col :span="3">
                  <el-button type="primary" >重置</el-button>
                </el-col>
            </el-row>
            <el-button type="success"  @click="addyonghuDialogVisible = true">新增</el-button>
            <el-button type="warning" @click="edityonghuDialogVisible= true">编辑</el-button> 
            <el-button type="danger"  @click="deletebumen">删除</el-button>
            <el-button type="info"  @click="rightDialogVisible= true">权限设置</el-button>
            <el-table :data="tableData" height="185" border style="width: 100%">
                <el-table-column type="selection" width="55"></el-table-column>
                <el-table-column type="index" width="50" fixed></el-table-column>
                <el-table-column prop="date" label="供应商编码" width="100"></el-table-column>
                <el-table-column prop="name" label="供应商名称" width="100"></el-table-column>
                <el-table-column prop="name" label="商品大类型" width="100"></el-table-column>
                <el-table-column prop="name" label="商品编号" width="100"></el-table-column>
                <el-table-column prop="name" label="商品小类型" width="100"></el-table-column>
                <el-table-column prop="name" label="品牌"></el-table-column>
                <el-table-column prop="name" label="克重"></el-table-column>
                <el-table-column prop="name" label="门幅"></el-table-column>
                <el-table-column prop="name" label="淋膜类型"></el-table-column>
                <el-table-column prop="name" label="状态" width="70"></el-table-column>
            </el-table>
             <el-table :data="tableData" height="185" border style="width: 100%">
                <el-table-column type="selection" width="55"></el-table-column>
                <el-table-column type="index" width="50" fixed></el-table-column>
                <el-table-column prop="date" label="供应商编码" width="100"></el-table-column>
                <el-table-column prop="name" label="供应商名称" width="100"></el-table-column>
                <el-table-column prop="name" label="商品大类型" width="100"></el-table-column>
                <el-table-column prop="name" label="商品编号" width="100"></el-table-column>
                <el-table-column prop="name" label="商品小类型" width="100"></el-table-column>
                <el-table-column prop="name" label="克重"></el-table-column>
                <el-table-column prop="name" label="状态" width="70"></el-table-column>
            </el-table>
             <el-table :data="tableData" height="185" border style="width: 100%">
                <el-table-column type="selection" width="55"></el-table-column>
                <el-table-column type="index" width="50" ></el-table-column>
                <el-table-column prop="date" label="供应商编码" width="100"></el-table-column>
                <el-table-column prop="name" label="供应商名称" width="100"></el-table-column>
                <el-table-column prop="name" label="商品大类型" width="100"></el-table-column>
                <el-table-column prop="name" label="商品编号" width="100"></el-table-column>
                <el-table-column prop="name" label="商品小类型" width="100"></el-table-column>
                <el-table-column prop="name" label="尺寸/长"></el-table-column>
                <el-table-column prop="name" label="尺寸/宽"></el-table-column>
                <el-table-column prop="name" label="尺寸/高"></el-table-column>
                <el-table-column prop="name" label="状态" width="70"></el-table-column>
            </el-table>
             <el-table :data="tableData" height="185" border style="width: 100%">
                <el-table-column type="selection" width="55"></el-table-column>
                <el-table-column type="index" width="50" ></el-table-column>
               <el-table-column prop="date" label="供应商编码" width="100"></el-table-column>
                <el-table-column prop="name" label="供应商名称" width="100"></el-table-column>
                <el-table-column prop="name" label="商品大类型" width="100"></el-table-column>
                <el-table-column prop="name" label="商品编号" width="100"></el-table-column>
                <el-table-column prop="name" label="淋膜类型"></el-table-column>
                <el-table-column prop="name" label="状态" width="70"></el-table-column>
            </el-table>
             <el-table :data="tableData" height="185" border style="width: 100%">
                <el-table-column type="selection" width="55"></el-table-column>
                <el-table-column type="index" width="50" ></el-table-column>
                <el-table-column prop="date" label="供应商编码" width="100"></el-table-column>
                <el-table-column prop="name" label="供应商名称" width="100"></el-table-column>
                <el-table-column prop="name" label="商品大类型" width="100"></el-table-column>
                <el-table-column prop="name" label="商品编号" width="100"></el-table-column>
                <el-table-column prop="name" label="宽度"></el-table-column>
                <el-table-column prop="name" label="颜色"></el-table-column>
                <el-table-column prop="name" label="状态" width="70"></el-table-column>
            </el-table>
          </el-col>
        </el-row>
      </el-card>
      <el-dialog
        title="新增供应商商品"
        :visible.sync="addyonghuDialogVisible"
        width="48%"
        :before-close="handleClose">
        <el-form :label-position="labelPosition" label-width="120px">
          <el-row>
            <el-col :span="12">
              <el-form-item label="供应商编号："><el-input placeholder="请输入供应商编号"></el-input></el-form-item>
              <el-form-item label="供应商名称："><el-input placeholder="请输入供应商名称"></el-input></el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item label="商品编号："><el-input placeholder="请输入商品编号"></el-input></el-form-item>
              <el-form-item label="状态：">
                <el-select class="tiantou" placeholder="请选择状态" v-model="value">
                  <el-option  value="纸张"></el-option>
                 </el-select>
              </el-form-item>
            </el-col>
          </el-row>
          <el-form-item label="商品大类型：">
                <el-select class="tiantou" placeholder="请选择商品大类型" @change="showshoop"  v-model="value">
                  <el-option value="纸张" id="show">纸张</el-option>
                  <el-option  value="纸箱" id="show">纸箱</el-option>
                  <el-option  value="袋子" id="show">袋子</el-option>
                  <el-option  value="油墨" id="show">油墨</el-option>
                  <el-option  value="胶带" id="show">胶带</el-option>
                 </el-select>
          </el-form-item>
          <div v-show="bigType == '纸张'">
            <el-form-item label="商品小类型："><el-input placeholder="请输入商品小类型" class="xiang"></el-input></el-form-item>          
            <el-form-item label="品牌："><el-input placeholder="请输入品牌" class="xiang"></el-input></el-form-item>
            <el-form-item label="克重："><el-input placeholder="请输入克重" class="xiang"></el-input></el-form-item>
            <el-form-item label="门幅："><el-input placeholder="请输入门幅" class="xiang"></el-input></el-form-item>
            <el-form-item label="淋膜类型："><el-input placeholder="请输入淋膜类型" class="xiang"></el-input></el-form-item>
          </div>
          <div v-show="bigType == '纸箱'">
            <el-form-item label="淋膜类型："><el-input placeholder="请输入淋膜类型" class="xiang"></el-input></el-form-item>
          </div>
          <div v-show="bigType == '袋子'">
            <el-form-item label="商品小类型："><el-input placeholder="请输入商品小类型" class="xiang"></el-input></el-form-item>          
            <el-form-item label="品牌："><el-input placeholder="请输入品牌" class="xiang"></el-input></el-form-item>
            <el-form-item label="克重："><el-input placeholder="请输入克重" class="xiang"></el-input></el-form-item>
            <el-form-item label="门幅："><el-input placeholder="请输入门幅" class="xiang"></el-input></el-form-item>
            <el-form-item label="淋膜类型："><el-input placeholder="请输入淋膜类型" class="xiang"></el-input></el-form-item>
          </div>
          <div v-show="bigType == '油墨'">
            <el-form-item label="克重："><el-input placeholder="请输入克重" class="xiang"></el-input></el-form-item>
          </div>
          <div v-show="bigType == '胶带'">
            <el-form-item label="尺寸/长："><el-input placeholder="请输入尺寸/长" class="xiang"></el-input></el-form-item>          
            <el-form-item label="颜色/宽："><el-input placeholder="请输入颜色/宽" class="xiang"></el-input></el-form-item>
            <el-form-item label="高："><el-input placeholder="请输入高" class="xiang"></el-input></el-form-item>
          </div>
          <div id="shoop">      
            <el-form-item label="宽度："><el-input placeholder="请输入宽度" class="xiang"></el-input></el-form-item>  
            <el-form-item label="颜色："><el-input placeholder="请输入颜色" class="xiang"></el-input></el-form-item>
          </div>
        </el-form>
        <span slot="footer" class="dialog-footer">
          <el-button @click="addyonghuDialogVisible = false">取 消</el-button>
          <el-button type="primary" @click="addyonghuDialogVisible = false">确 定</el-button>
        </span>
      </el-dialog>
      <el-dialog
        title="编辑供应商商品"
        :visible.sync="edityonghuDialogVisible"
        width="48%"
        :before-close="handleClose">
        <el-form :label-position="labelPosition" label-width="120px">
          <el-row>
            <el-col :span="12">
              <el-form-item label="供应商编号："><el-input placeholder="请输入供应商编号"></el-input></el-form-item>
              <el-form-item label="供应商名称："><el-input placeholder="请输入供应商名称"></el-input></el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item label="商品编号："><el-input placeholder="请输入商品编号"></el-input></el-form-item>
              <el-form-item label="状态：">
                <el-select class="tiantou" placeholder="请选择状态" v-model="value">
                  <el-option  value="纸张"></el-option>
                 </el-select>
              </el-form-item>
            </el-col>
          </el-row>
          <el-form-item label="商品大类型：">
                <el-select class="tiantou" placeholder="请选择商品大类型" @change="showshoop"  v-model="value">
                  <el-option value="纸张" id="show">纸张</el-option>
                  <el-option  value="纸箱" id="show">纸箱</el-option>
                  <el-option  value="袋子" id="show">袋子</el-option>
                  <el-option  value="油墨" id="show">油墨</el-option>
                  <el-option  value="胶带" id="show">胶带</el-option>
                 </el-select>
          </el-form-item>
          <div v-show="bigType == '纸张'">
            <el-form-item label="商品小类型："><el-input placeholder="请输入商品小类型" class="xiang"></el-input></el-form-item>          
            <el-form-item label="品牌："><el-input placeholder="请输入品牌" class="xiang"></el-input></el-form-item>
            <el-form-item label="克重："><el-input placeholder="请输入克重" class="xiang"></el-input></el-form-item>
            <el-form-item label="门幅："><el-input placeholder="请输入门幅" class="xiang"></el-input></el-form-item>
            <el-form-item label="淋膜类型："><el-input placeholder="请输入淋膜类型" class="xiang"></el-input></el-form-item>
          </div>
          <div v-show="bigType == '纸箱'">
            <el-form-item label="淋膜类型："><el-input placeholder="请输入淋膜类型" class="xiang"></el-input></el-form-item>
          </div>
          <div v-show="bigType == '袋子'">
            <el-form-item label="商品小类型："><el-input placeholder="请输入商品小类型" class="xiang"></el-input></el-form-item>          
            <el-form-item label="品牌："><el-input placeholder="请输入品牌" class="xiang"></el-input></el-form-item>
            <el-form-item label="克重："><el-input placeholder="请输入克重" class="xiang"></el-input></el-form-item>
            <el-form-item label="门幅："><el-input placeholder="请输入门幅" class="xiang"></el-input></el-form-item>
            <el-form-item label="淋膜类型："><el-input placeholder="请输入淋膜类型" class="xiang"></el-input></el-form-item>
          </div>
          <div v-show="bigType == '油墨'">
            <el-form-item label="克重："><el-input placeholder="请输入克重" class="xiang"></el-input></el-form-item>
          </div>
          <div v-show="bigType == '胶带'">
            <el-form-item label="尺寸/长："><el-input placeholder="请输入尺寸/长" class="xiang"></el-input></el-form-item>          
            <el-form-item label="颜色/宽："><el-input placeholder="请输入颜色/宽" class="xiang"></el-input></el-form-item>
            <el-form-item label="高："><el-input placeholder="请输入高" class="xiang"></el-input></el-form-item>
          </div>
          <div id="shoop">      
            <el-form-item label="宽度："><el-input placeholder="请输入宽度" class="xiang"></el-input></el-form-item>  
            <el-form-item label="颜色："><el-input placeholder="请输入颜色" class="xiang"></el-input></el-form-item>
          </div>
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
       value:'',
       labelPosition: 'right',
       addyonghuDialogVisible: false,
       edityonghuDialogVisible:false,
       resetPassdialogVisible:false,
       bigType: '',
       tableData: [{
          date: '2016-05-03',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        }, {
          date: '2016-05-02',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        }, {
          date: '2016-05-04',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        }, {
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        }, {
          date: '2016-05-08',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        }, {
          date: '2016-05-06',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        }, {
          date: '2016-05-07',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        }]
    }
  },
  created () {
  },
  methods:{
    showshoop(value){
      console.log(value);
      this.bigType = value;
      // document.getElementById("shoop").style.display = "block";
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
     .quan{
      height: 1170px;
      float: left;
      margin-right: 20px;
    }

    .togglr-button{
      width: 120px;
      height: 30px;
      background: #eee;
      text-align: center;
      line-height: 30px;
    }
    .el-pagination{
        margin-top: 30px;
    }
    .el-button{
      margin-top: 10px;
    }
    .shu{
        .el-button{
            display: block;
            margin: 0px;
            padding:10px;
            font-size: 16px;
            color: #999;
        }
        .el-button:hover{
            color: #666;
            
        }
    }
    #shoop{
      display: none;
    }
</style>
