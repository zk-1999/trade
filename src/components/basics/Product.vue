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
                <el-form :inline="true" class="demo-form-inline" :model="chaProductForm" ref="chaProductRef">
                    <el-form-item label="设计稿编码：" prop="designName">
                    <el-input placeholder="请输入名称" v-model="chaProductForm.designName"></el-input>
                    </el-form-item>
                    <el-form-item label="颜色：" prop="designCol1">
                    <el-input placeholder="请输入颜色" v-model="chaProductForm.designCol1"></el-input>
                    </el-form-item>
                    <el-form-item label="状态：" prop="designState">
                    <el-select v-model="chaProductForm.designState" placeholder="请选择">
                      <el-option
                        v-for="item in chaproductList"
                        :key="item.designId"
                        :label="item.a"
                        :value="item.designState">
                      </el-option>
                    </el-select>
                    </el-form-item>
                    <el-form-item>
                        <el-button @click="getProductList">查询</el-button>
                        <el-button type="primary" @click="chaProductResetForm">重置</el-button>
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
          <el-table border stripe :data="productList" @selection-change="handleSelectionChange">
            <el-table-column type="selection" width="50" align="center"></el-table-column>
            <el-table-column type="index" width="50" align="center"></el-table-column>
            <el-table-column prop="" label="设计稿编码" align="center">
              <template slot-scope="scope">
                {{scope.row.designModel+'-'+scope.row.designDate+'-'+scope.row.designName}}
              </template>
            </el-table-column>
            <!-- <el-table-column prop="b" label="名称"></el-table-column> -->
            <el-table-column prop="" label="颜色" align="center">
              <template slot-scope="scope">
                <!-- {{scope.row.designCol2}} -->
                <el-tag v-if="scope.row.designCol1!=''&&scope.row.designCol1!=null">{{scope.row.designCol1}}</el-tag>
                <el-tag type="success" v-if="scope.row.designCol2!=''&&scope.row.designCol2!=null">{{scope.row.designCol2}}</el-tag>
                <el-tag type="info" v-if="scope.row.designCol3!=''&&scope.row.designCol3!=null">{{scope.row.designCol3}}</el-tag>
                <el-tag type="warning" v-if="scope.row.designCol4!=''&&scope.row.designCol4!=null">{{scope.row.designCol4}}</el-tag> 
                </br>
                <el-tag v-if="scope.row.designCol5!=''&&scope.row.designCol5!=null">{{scope.row.designCol5}}</el-tag>
                <el-tag type="success" v-if="scope.row.designCol6!=''&&scope.row.designCol6!=null">{{scope.row.designCol6}}</el-tag>
                <el-tag type="info" v-if="scope.row.designCol7!=''&&scope.row.designCol7!=null">{{scope.row.designCol7}}</el-tag>
                <el-tag type="warning" v-if="scope.row.designCol8!=''&&scope.row.designCol8!=null">{{scope.row.designCol8}}</el-tag>
                <!-- {{scope.row.designCol1==null?'':scope.row.designCol1+','+scope.row.designCol2+','+scope.row.designCol3+','+scope.row.designCol4+','+
                scope.row.designCol5+','+scope.row.designCol6+','+scope.row.designCol7+','+scope.row.designCol8}} -->
              </template>
            </el-table-column>
            <el-table-column prop="" label="图片" align="center">
              <!-- <el-image
                style="width: 200px; height: 100px"
                :src="url"
                ></el-image> -->
                <div class="demo-image__preview">
                  <el-image
                    style="width:200px; height: 100px"
                    :src="url" 
                    :preview-src-list="srcList"
                    >
                  </el-image>
                </div>
            </el-table-column>
            <el-table-column label="状态" width="65px" align="center">
              <template slot-scope="scope">
                <el-switch
                  v-model="scope.row.designState"
                  active-color="#13ce66"
                  inactive-color="#ff4949"
                  :active-value="1"
                  :inactive-value="0"
                  @change="userStateChanged(scope.row)"
                ></el-switch>
              </template>
            </el-table-column>
            <el-table-column label="操作" width="190px" align="center">
              <template slot-scope="scope">
                <el-button type="primary" icon="el-icon-edit" size="mini" @click="showProduct(scope.row.designId)">修改</el-button>
                <el-button
                  type="danger"
                  icon="el-icon-delete"
                  @click="deletebumen(scope.row.designId)"
                  size="mini"
                >删除</el-button>
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
        title="新增产品设计稿"
        :visible.sync="addyonghuDialogVisible"
        width="40%"
        :before-close="handleClose">
        <el-form :label-position="labelPosition" label-width="120px" :model="addProductForm"
        ref="addProductRef"
        :rules="addProductRules">
            <el-form-item label="产品型号：" prop="designModel"><el-input placeholder="请输入产品型号" v-model="addProductForm.designModel"></el-input></el-form-item>      
            <el-form-item label="产品日期：" prop="designDate"><el-input placeholder="请输入产品日期" v-model="addProductForm.designDate"></el-input></el-form-item>
            <el-form-item label="产品名称：" prop="designName"><el-input placeholder="请输入产品名称" v-model="addProductForm.designName"></el-input></el-form-item>      

              <el-row>
                <el-col :span="12">
                  <el-form-item label="颜色：" prop="designCol1">
                   <el-input placeholder="请输入颜色1" v-model="addProductForm.designCol1"></el-input>
                   </el-form-item>
                   <el-form-item prop="designCol2">
                   <el-input placeholder="请输入颜色2" v-model="addProductForm.designCol2"></el-input>
                   </el-form-item>
                   <el-form-item prop="designCol3">
                   <el-input placeholder="请输入颜色3" v-model="addProductForm.designCol3"></el-input>
                   </el-form-item>
                   <el-form-item prop="designCol4">
                   <el-input placeholder="请输入颜色4" v-model="addProductForm.designCol4"></el-input>
                   </el-form-item>
                </el-col>
                 <el-col :span="12">
                   <el-form-item label-width="0px" prop="designCol5">
                   <el-input placeholder="请输入颜色5" v-model="addProductForm.designCol5"></el-input>
                   </el-form-item>
                   <el-form-item label-width="0px" prop="designCol6">
                   <el-input placeholder="请输入颜色6" v-model="addProductForm.designCol6"></el-input>
                   </el-form-item>
                   <el-form-item label-width="0px" prop="designCol7">
                   <el-input placeholder="请输入颜色7" v-model="addProductForm.designCol7"></el-input>
                   </el-form-item>
                   <el-form-item label-width="0px" prop="designCol8">
                   <el-input placeholder="请输入颜色8" v-model="addProductForm.designCol8"></el-input>
                   </el-form-item>
                </el-col>
               </el-row>
            
            <el-form-item label="上传设计稿：" prop="designPicture">
             <el-upload
              action="https://jsonplaceholder.typicode.com/posts/"
              list-type="picture-card"
              :on-preview="handlePictureCardPreview"
              :on-remove="handleRemove">
              <i class="el-icon-plus"></i>
            </el-upload>
            </el-form-item>
        </el-form>
        <span slot="footer" class="dialog-footer">
          <el-button @click="addyonghuDialogVisible = false">取 消</el-button>
          <el-button type="primary" @click="addProduct">确 定</el-button>
        </span>
      </el-dialog>
      <el-dialog
        title="编辑产品设计稿"
        :visible.sync="edityonghuDialogVisible"
        width="40%"
        :before-close="handleClose">
        <el-form :label-position="labelPosition" label-width="120px" :model="editProductForm"
        ref="editProductRef"
        :rules="addProductRules">
            <el-form-item label="产品型号：" prop="designModel"><el-input placeholder="请输入产品型号" v-model="editProductForm.designModel"></el-input></el-form-item>      
            <el-form-item label="产品日期：" prop="designDate"><el-input placeholder="请输入产品日期" v-model="editProductForm.designDate"></el-input></el-form-item>
            <el-form-item label="产品名称：" prop="designName"><el-input placeholder="请输入产品名称" v-model="editProductForm.designName"></el-input></el-form-item>      
              <el-row>
                <el-col :span="12">
                  <el-form-item label="颜色：" prop="designCol1">
                   <el-input placeholder="请输入颜色1" v-model="editProductForm.designCol1"></el-input>
                   </el-form-item>
                   <el-form-item prop="designCol2">
                   <el-input placeholder="请输入颜色2" v-model="editProductForm.designCol2"></el-input>
                   </el-form-item>
                   <el-form-item prop="designCol3">
                   <el-input placeholder="请输入颜色3" v-model="editProductForm.designCol3"></el-input>
                   </el-form-item>
                   <el-form-item prop="designCol4">
                   <el-input placeholder="请输入颜色4" v-model="editProductForm.designCol4"></el-input>
                   </el-form-item>
                </el-col>
                 <el-col :span="12">
                   <el-form-item label-width="0px" prop="designCol5">
                   <el-input placeholder="请输入颜色5" v-model="editProductForm.designCol5"></el-input>
                   </el-form-item>
                   <el-form-item label-width="0px" prop="designCol6">
                   <el-input placeholder="请输入颜色6" v-model="editProductForm.designCol6"></el-input>
                   </el-form-item>
                   <el-form-item label-width="0px" prop="designCol7">
                   <el-input placeholder="请输入颜色7" v-model="editProductForm.designCol7"></el-input>
                   </el-form-item>
                   <el-form-item label-width="0px" prop="designCol8">
                   <el-input placeholder="请输入颜色8" v-model="editProductForm.designCol8"></el-input>
                   </el-form-item>
                </el-col>
               </el-row>
            
            <el-form-item label="上传设计稿：" prop="designPicture">
              <el-upload
                action="https://jsonplaceholder.typicode.com/posts/"
                list-type="picture-card"
                :on-preview="handlePictureCardPreview"
                :on-remove="handleRemove">
                <i class="el-icon-plus"></i>
              </el-upload>
            </el-form-item>
        </el-form>
        <span slot="footer" class="dialog-footer">
          <el-button @click="edityonghuDialogVisible = false">取 消</el-button>
          <el-button type="primary" @click="editProduct">确 定</el-button>
        </span>
      </el-dialog>
      <el-dialog :visible.sync="dialogVisible">
        <img width="100%" :src="dialogImageUrl" alt="">
      </el-dialog>
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
    <el-dialog :visible.sync="dialogVisible">
  <img width="100%" :src="dialogImageUrl" alt="">
</el-dialog>
    </div>
</template>
<script>
export default {
  data () {
    return {
      dialogImageUrl: '',
      dialogVisible: false,
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
      delarr:[],
      productList:[],
      
      dialogImageUrl: '',
      dialogVisible: false,
      chaproductList:[{designState:1,a:'启用',designId:0},{designState:0,a:'禁用',designId:1}],
      chaProductForm:{
        designName:'',
        designCol1:'',
        designState:'',
      },
      addProductForm:{
        designName:'',
        designModel:'',
        designDate:'',
        designPicture:'',
        designCol1:'',
        designCol2:'',
        designCol3:'',
        designCol4:'',
        designCol5:'',
        designCol6:'',
        designCol7:'',
        designCol8:'',
      },
      editProductForm:{
        designName:'',
        designModel:'',
        designDate:'',
        designPicture:'',
        designCol1:'',
        designCol2:'',
        designCol3:'',
        designCol4:'',
        designCol5:'',
        designCol6:'',
        designCol7:'',
        designCol8:'',
      },
      addProductRules: {
          designName:[
          { required: true, message: '请输入用户名', trigger: 'blur' },
          { min: 3, max: 10, message: '长度在 3 到 10 个字符', trigger: 'blur' }
          ],},
      url: 'https://fuss10.elemecdn.com/e/5d/4a731a90594a4af544c0c25941171jpeg.jpeg',
      srcList: [
          'https://fuss10.elemecdn.com/e/5d/4a731a90594a4af544c0c25941171jpeg.jpeg',
          'https://fuss10.elemecdn.com/e/5d/4a731a90594a4af544c0c25941171jpeg.jpeg'
        ]
    }
  },
  created () {
    this.getProductList();
  },
  methods:{
    async getProductList(){
      const { data: res } = await this.$http.post("jc/Design/selectDesign",this.chaProductForm);
      console.log(res);
      // console.log(this.chamerchandiseForm);
      
      this.productList = res;
    },
    async userStateChanged(userInfo) {
      const { data: res } = await this.$http.post("jc/Design/updatedesignstate",userInfo);
      this.getProductList();
    },
    chaProductResetForm(formName){
        this.$refs.chaProductRef.resetFields();
        this.getProductList();
    },
    addProduct() {
      this.$refs.addProductRef.validate(async valid => {
        if (!valid) return;    
        const { data: res } = await this.$http.post("jc/Design/addDesign",this.addProductForm);
        this.$message.success("用户创建成功！");
        this.getProductList();
        this.addyonghuDialogVisible = false;
      });
    },
    async showProduct(designId){
      let param = new URLSearchParams();
      param.append("designId", designId);
      const {data:res} = await this.$http.post('jc/Design/selectDesignByid',param);
      console.log(res);
      this.editProductForm=res;
      this.edityonghuDialogVisible=true;
    },
    async editProduct(){
       const {data:res} = await this.$http.post('jc/Design/updateDesign',this.editProductForm);
       this.getProductList();
       this.edityonghuDialogVisible=false;
    },
    selectedqi(){
      this.delarr=[];
      this.delVisibleqi = true;
      for (let i = 0; i < this.selectedList.length; i++) {
        this.delarr.push({designId:this.selectedList[i].designId,designState:this.selectedList[i].designState==1?0:1})
      }
      console.log(this.delarr);
    },
    selected(){
      this.delarr=[];
      this.delVisible = true;
      for (let i = 0; i < this.selectedList.length; i++) {
        this.delarr.push(this.selectedList[i].designId)
      }
      console.log(this.delarr);
    },
    async deleteRow(){
         const {data:res} = await this.$http.post('jc/Design/deleteDesignmore',this.delarr);
         this.delVisible = false;
         this.getProductList();
      },
      async deleteRowqi(){
         const {data:res} = await this.$http.post('jc/Design/updatedesignmorestate',this.delarr);
         this.delVisibleqi = false;
         this.getProductList();
      },
     handleRemove(file, fileList) {
        console.log(file, fileList);
      },
      handlePictureCardPreview(file) {
        this.dialogImageUrl = file.url;
        this.dialogVisible = true;
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
    deletebumen(designId){
      this.$confirm('此操作将永久删除该职务, 是否继续?', '提示', {
          confirmButtonText: '确定',
          cancelButtonText: '取消',
          type: 'warning'
        }).then(async() => {
          let param = new URLSearchParams();
        param.append("designId", designId);
        const { data: res } = await this.$http.post(
          "jc/Design/deleteDesign",
          param
        );
        this.getProductList();
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
    .el-tag{
      margin: 5px 15px;
    }
    .el-form-item{
      margin-bottom: 15px;
    }
</style>