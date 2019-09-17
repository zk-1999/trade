<template>
  <div class="min1500">
    <!-- 面包屑导航区域 -->
    <el-breadcrumb separator-class="el-icon-arrow-right">
      <el-breadcrumb-item :to="{ path: '/welcome' }">首页</el-breadcrumb-item>
      <el-breadcrumb-item>基础资料</el-breadcrumb-item>
      <el-breadcrumb-item>供应商管理</el-breadcrumb-item>
    </el-breadcrumb>
    <el-card>
      <el-row :gutter="20" class="row">
        <el-col :span="24">
          <el-row :gutter="20">
            <el-form :inline="true" class="demo-form-inline" :model="chaSupplierForm" ref="chaSupplierRef">
              <el-form-item label="供应商名称：" prop="supName">
                <el-input placeholder="请输入供应商名称" v-model="chaSupplierForm.supName"></el-input>
              </el-form-item>
              <el-form-item label="类型：" prop="supType">
                <el-input placeholder="请输入类型" v-model="chaSupplierForm.supType"></el-input>
              </el-form-item>
              <el-form-item label="联系人：" prop="supContacts">
                <el-input placeholder="请输入联系人" v-model="chaSupplierForm.supContacts"></el-input>
              </el-form-item>
              <el-form-item label="联系人手机：" prop="supPhone">
                <el-input placeholder="请输入联系人手机" v-model="chaSupplierForm.supPhone"></el-input>
              </el-form-item>
              <el-form-item>
                <el-button @click="getSupplierList">查询</el-button>
                <el-button type="primary"  @click="chaSupplierResetForm('chaSupplierForm')">重置</el-button>
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
          <el-table border :data="supplierList" stripe @selection-change="handleSelectionChange">
            <el-table-column type="selection" width="55"></el-table-column>
            <el-table-column type="index"></el-table-column>
            <el-table-column prop="supId" label="供应商编码"></el-table-column>
            <el-table-column prop="supName" label="供应商名称"></el-table-column>
            <el-table-column prop="supType" label="类型"></el-table-column>
            <el-table-column prop="supContacts" label="联系人"></el-table-column>
            <el-table-column prop="supPhone" label="联系人手机"></el-table-column>
            <!-- <el-table-column prop="supState" label="状态"></el-table-column> -->
            <el-table-column prop="supCreateUser" label="创建人"></el-table-column>
            <el-table-column prop="supCreateTime" label="创建时间"></el-table-column>
            <el-table-column prop="supState" label="状态" width="65px">
              <template slot-scope="scope">
                <!-- {{scope.row}} -->
                <el-switch
                  v-model="scope.row.supState"
                  active-color="#13ce66"
                  inactive-color="#ff4949"
                  :active-value="1"
                  :inactive-value="0"
                  @change="userStateChanged(scope.row)"
                ></el-switch>
              </template>
            </el-table-column>
            <el-table-column label="操作" width="190px">
              <template slot-scope="scope">
                <el-button type="primary" icon="el-icon-edit" size="mini" @click="showEditSupplier(scope.row.supplierId)">修改</el-button>
                <el-button
                  type="danger"
                  icon="el-icon-delete"
                  @click="deletebumen(scope.row.supplierId)"
                  size="mini"
                >删除</el-button>
              </template>
            </el-table-column>
          </el-table>
        </el-col>
      </el-row>
      <el-pagination
        @size-change="handleSizeChange"
        @current-change="handleCurrentChange"
        :current-page="currentPage4"
        :page-sizes="[100, 200, 300, 400]"
        :page-size="100"
        layout="total, sizes, prev, pager, next, jumper"
        :total="400"
      ></el-pagination>
    </el-card>
    <el-dialog
      title="新增供应商"
      :visible.sync="addyonghuDialogVisible"
      width="48%"
      :before-close="handleClose"
    >
      <el-form
        :label-position="labelPosition"
        :model="addSupplierForm"
        ref="addSupplierRef"
        label-width="120px"
        :rules="addsSupplierRules"
      >
        <el-row>
          <el-col :span="12">
            <el-form-item label="供应商编码：" prop="supId">
              <el-input v-model="addSupplierForm.supId" placeholder="供应商编码"></el-input>
            </el-form-item>
            <el-form-item label="联系人：" prop="supContacts">
              <el-input v-model="addSupplierForm.supContacts" placeholder="请输入联系人"></el-input>
            </el-form-item>
            <el-form-item label="联系邮箱：" prop="supEmail">
              <el-input v-model="addSupplierForm.supEmail" placeholder="请输入联系邮箱"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="12">
            <el-form-item label="供应商名称：" prop="supName">
              <el-input v-model="addSupplierForm.supName" placeholder="请输入供应商名称"></el-input>
            </el-form-item>
            <el-form-item label="联系人手机：" prop="supPhone">
              <el-input v-model="addSupplierForm.supPhone" placeholder="请输入联系人手机"></el-input>
            </el-form-item>
            <el-form-item label="类型：" prop="selectsup">
              <el-select class="tiantou" v-model="selectsup" placeholder="请选择类型">
                <el-option
              v-for="item in options"
              :key="item.value"
              :label="item.label"
              :value="item.value"
            ></el-option>
              </el-select>
            </el-form-item>
          </el-col>
        </el-row>
        <el-form-item label="联系地址：">
         <el-select placeholder="省级地区" v-model="selectsup" class="hu">
            <el-option
              v-for="item in options"
              :key="item.value"
              :label="item.label"
              :value="item.value"
            ></el-option>
          </el-select>
          <el-select placeholder="市级地区" v-model="selectsup" class="hu">
            <el-option
              v-for="item in options"
              :key="item.value"
              :label="item.label"
              :value="item.value"
            ></el-option>
          </el-select>
          <el-select placeholder="区级地区" v-model="selectsup" class="hu">
            <el-option
              v-for="item in options"
              :key="item.value"
              :label="item.label"
              :value="item.value"
            ></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="详细地址：" prop="supAddress">
          <el-input v-model="addSupplierForm.supAddress" placeholder="请输入详细地址" class="xiang"></el-input>
        </el-form-item>
        <el-form-item label="银行卡号：" prop="supBank">
          <el-input v-model="addSupplierForm.supBank" placeholder="请输入银行卡号" class="xiang"></el-input>
        </el-form-item>
      </el-form>
      <span slot="footer" class="dialog-footer">
        <el-button @click="addyonghuDialogVisible = false">取 消</el-button>
        <el-button type="primary" @click="addSupplier">确 定</el-button>
      </span>
    </el-dialog>
    <el-dialog
      title="编辑供应商"
      :visible.sync="edityonghuDialogVisible"
      width="48%"
      :before-close="handleClose"
    >
       <el-form
        :label-position="labelPosition"
        :model="editSupplierForm"
        ref="addSupplierRef"
        label-width="120px"
        :rules="addsSupplierRules"
      >
        <el-row>
          <el-col :span="12">
            <el-form-item label="供应商编码：" prop="supId">
              <el-input v-model="editSupplierForm.supId" placeholder="供应商编码"></el-input>
            </el-form-item>
            <el-form-item label="联系人：" prop="supContacts">
              <el-input v-model="editSupplierForm.supContacts" placeholder="请输入联系人"></el-input>
            </el-form-item>
            <el-form-item label="联系邮箱：" prop="supEmail">
              <el-input v-model="editSupplierForm.supEmail" placeholder="请输入联系邮箱"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="12">
            <el-form-item label="供应商名称：" prop="supName">
              <el-input v-model="editSupplierForm.supName" placeholder="请输入供应商名称"></el-input>
            </el-form-item>
            <el-form-item label="联系人手机：" prop="supPhone">
              <el-input v-model="editSupplierForm.supPhone" placeholder="请输入联系人手机"></el-input>
            </el-form-item>
            <el-form-item label="类型：" prop="selectsup">
              <el-select class="tiantou" v-model="selectsup" placeholder="请选择类型">
                <el-option
              v-for="item in options"
              :key="item.value"
              :label="item.label"
              :value="item.value"
            ></el-option>
              </el-select>
            </el-form-item>
          </el-col>
        </el-row>
        <el-form-item label="联系地址：">
         <el-select placeholder="省级地区" v-model="selectsup" class="hu">
            <el-option
              v-for="item in options"
              :key="item.value"
              :label="item.label"
              :value="item.value"
            ></el-option>
          </el-select>
          <el-select placeholder="市级地区" v-model="selectsup" class="hu">
            <el-option
              v-for="item in options"
              :key="item.value"
              :label="item.label"
              :value="item.value"
            ></el-option>
          </el-select>
          <el-select placeholder="区级地区" v-model="selectsup" class="hu">
            <el-option
              v-for="item in options"
              :key="item.value"
              :label="item.label"
              :value="item.value"
            ></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="详细地址：" prop="supAddress">
          <el-input v-model="editSupplierForm.supAddress" placeholder="请输入详细地址" class="xiang"></el-input>
        </el-form-item>
        <el-form-item label="银行卡号：" prop="supBank">
          <el-input v-model="editSupplierForm.supBank" placeholder="请输入银行卡号" class="xiang"></el-input>
        </el-form-item>
      </el-form>
      <span slot="footer" class="dialog-footer">
        <el-button @click="edityonghuDialogVisible = false">取 消</el-button>
        <el-button type="primary" @click="editSupplier">确 定</el-button>
      </span>
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
  </div>
</template>
<script>
import { async } from "q";
export default {
  data() {
    return {
      // a:'0',
      labelPosition: "right",
      addyonghuDialogVisible: false,
      edityonghuDialogVisible: false,
      resetPassdialogVisible: false,
      delVisible:false,
      delVisibleqi:false,
      currentPage1: 5,
      currentPage2: 5,
      currentPage3: 5,
      currentPage4: 4,
      selectedList: [],
      delarr:[],
      supplierList: [],
      addSupplierForm: {
        supId: "",
        supName: "",
        supType: "",
        supContacts: "",
        supPhone: "",
        supEmail: "",
        supCreateUser: "",
        supCreateTime: "",
        supPriv: "",
        supCity: "",
        supTown: "",
        supAddress: "",
        supBank: ""
      },
      editSupplierForm: {
        supId: "",
        supName: "",
        supType: "",
        supContacts: "",
        supPhone: "",
        supEmail: "",
        supCreateUser: "",
        supCreateTime: "",
        supPriv: "",
        supCity: "",
        supTown: "",
        supAddress: "",
        supBank: ""
      },
      chaSupplierForm: {
        supName: "",
        supType: "",
        supContacts: "",
        supPhone: "",
      },
      addsSupplierRules: {
          supName:[
          { required: true, message: '请输入用户名', trigger: 'blur' },
          { min: 3, max: 10, message: '长度在 3 到 10 个字符', trigger: 'blur' }
          ],},
      options: [
        {
          value: "选项1",
          label: "黄金糕"
        },
        {
          value: "选项2",
          label: "双皮奶"
        },
        {
          value: "选项3",
          label: "蚵仔煎"
        },
        {
          value: "选项4",
          label: "龙须面"
        },
        {
          value: "选项5",
          label: "北京烤鸭"
        }
      ],
      selectsup: ""
    };
  },
  created() {
    this.getSupplierList();
  },
  methods: {
    async getSupplierList() {
      const { data: res } = await this.$http.get("jc/supplier/selectSupplier",{params:this.chaSupplierForm});
      console.log(res);
      this.supplierList = res;
    },
    async userStateChanged(userInfo) {
      const { data: res } = await this.$http.post("jc/supplier/startSuppiler",userInfo);
      this.getSupplierList();
    },
    addSupplier() {
      this.$refs.addSupplierRef.validate(async valid => {
        if (!valid) return;    
        const { data: res } = await this.$http.post("/jc/supplier/addSupplier",this.addSupplierForm);
        this.$message.success("用户创建成功！");
        this.getSupplierList();
        this.addyonghuDialogVisible = false;
      });
    },
   async showEditSupplier(supplierId){
           let param = new URLSearchParams();
          param.append("supplierId", supplierId);
      const {data:res} = await this.$http.post('jc/supplier/selectSupplierbyid/',param);
      console.log(res);
      this.editSupplierForm=res;
      this.edityonghuDialogVisible=true;
    },
    async editSupplier(){
       const {data:res} = await this.$http.post('/jc/supplier/updateSupplier',this.editSupplierForm);
       this.getSupplierList();
       this.edityonghuDialogVisible=false;
    },
    chaSupplierResetForm(formName){
        this.$refs.chaSupplierRef.resetFields();
    },
    handleSelectionChange(val) {
      this.selectedList = val
    },
    
    handleSizeChange(val) {
      console.log(`每页 ${val} 条`);
    },
    handleCurrentChange(val) {
      console.log(`当前页: ${val}`);
    },
    handleClose(done) {
      this.$confirm("确认关闭？")
        .then(_ => {
          done();
        })
        .catch(_ => {});
    },
    selectedqi(){
      this.delVisibleqi = true;
      console.log(this.selectedList);
      console.log('------------------------');
      for (let i = 0; i < this.selectedList.length; i++) {
        this.delarr.push({supplierId:this.selectedList[i].supplierId,supState:this.selectedList[i].supState==1?0:1})
      }
      console.log(this.delarr);
    },
    selected(){
      this.delVisible = true;
      console.log(this.selectedList);
      console.log('------------------------');
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
    deletebumen(supplierId) {
      this.$confirm("此操作将永久删除该职务, 是否继续?", "提示", {
        confirmButtonText: "确定",
        cancelButtonText: "取消",
        type: "warning"
      })
        .then(async () => {
          let param = new URLSearchParams();
          param.append("supplierId", supplierId);
          const { data: res } = await this.$http.post(
            "/jc/supplier/deleteSupplier",
            param
          );
          console.log(supplierId);
          this.getSupplierList();

          this.$message({
            type: "success",
            message: "删除成功!"
          });
        })
        .catch(() => {
          this.$message({
            type: "info",
            message: "已取消删除"
          });
        });
    },
    handleNodeClick(data) {
      console.log(data);
    }
  }
};
</script>
<style lang='less' scoped>
.el-card {
  margin-top: 15px;
}
.el-row {
  align-items: center;
  display: flex;
}
.el-table {
  margin-top: 15px;
}
.demo-form-inline .el-input {
  width: 170px;
}
.el-select {
  width: 225px;
}
.xiang {
  width: 400px;
}
.hu {
  width: 133px;
}
</style>