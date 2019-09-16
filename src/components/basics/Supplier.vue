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
            <el-form :inline="true" class="demo-form-inline">
              <el-form-item label="供应商名称：">
                <el-input placeholder="请输入供应商名称"></el-input>
              </el-form-item>
              <el-form-item label="类型：">
                <el-input placeholder="请输入类型"></el-input>
              </el-form-item>
              <el-form-item label="联系人：">
                <el-input placeholder="请输入联系人"></el-input>
              </el-form-item>
              <el-form-item label="联系人手机：">
                <el-input placeholder="请输入联系人手机"></el-input>
              </el-form-item>
              <el-form-item>
                <el-button>查询</el-button>
                <el-button type="primary">重置</el-button>
              </el-form-item>
            </el-form>
          </el-row>
          <el-button type="success" @click="addyonghuDialogVisible = true">新增</el-button>
          <el-button
            type="warning"
            @click="editbumenDialogVisible= true"
            :disabled="selectedList.length == 0"
          >批量启用</el-button>
          <el-button
            type="warning"
            @click="editbumenDialogVisible= true"
            :disabled="selectedList.length == 0"
          >批量禁用</el-button>
          <el-button type="danger" @click="deletebumen" :disabled="selectedList.length == 0">批量删除</el-button>
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
                <el-button type="primary" icon="el-icon-edit" size="mini">修改</el-button>
                <el-button
                  type="danger"
                  icon="el-icon-delete"
                  @click="deletebumen(scope.row.supId)"
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
      <el-form :label-position="labelPosition" label-width="120px">
        <el-row>
          <el-col :span="12">
            <el-form-item label="供应商编码：">
              <el-input placeholder="供应商编码"></el-input>
            </el-form-item>
            <el-form-item label="联系人：">
              <el-input placeholder="请输入联系人"></el-input>
            </el-form-item>
            <el-form-item label="联系邮箱：">
              <el-input placeholder="请输入联系邮箱"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="12">
            <el-form-item label="供应商名称：">
              <el-input placeholder="请输入供应商名称"></el-input>
            </el-form-item>
            <el-form-item label="联系人手机：">
              <el-input placeholder="请输入联系人手机"></el-input>
            </el-form-item>
            <el-form-item label="类型：">
              <el-select class="tiantou" placeholder="请选择类型">
                <el-option></el-option>
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
        <el-form-item label="详细地址：">
          <el-input placeholder="请输入详细地址" class="xiang"></el-input>
        </el-form-item>
        <el-form-item label="银行卡号：">
          <el-input placeholder="请输入银行卡号" class="xiang"></el-input>
        </el-form-item>
      </el-form>
      <span slot="footer" class="dialog-footer">
        <el-button @click="edityonghuDialogVisible = false">取 消</el-button>
        <el-button type="primary" @click="edityonghuDialogVisible = false">确 定</el-button>
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
      currentPage1: 5,
      currentPage2: 5,
      currentPage3: 5,
      currentPage4: 4,
      selectedList: [],
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
      const { data: res } = await this.$http.get("jc/supplier/selectSupplier");
      console.log(res);
      this.supplierList = res;
      // if(res.meta.status !==200) return this.message.error('获取用户列表失败');
    },
    async userStateChanged(userInfo) {
      console.log(userInfo);

      let param = new URLSearchParams();
      param.append("supId", userInfo.supId);
      param.append("supState", userInfo.supState);

      // // if(userInfo.supState=true){
      // // param.append("supState", 1);
      // // }else{
      // // param.append("supState", 0);

      // // }
      const { data: res } = await this.$http.post(
        "/jc/supplier/startSupplier",
        param
      );
      this.getSupplierList();
      // if (res.code ==500) {
      //   // userInfo.mg_state = !userInfo.mg_state;
      //   return this.$message.error('更新用户状态失败！')
      // }
      // this.$message.success('更新用户状态成功！')
    },
    addSupplier() {
      
      this.$refs.addSupplierRef.validate(async valid => {
        if (!valid) return;
        console.log(this.addSupplierForm);

        const { data: res } = await this.$http.post("/jc/supplier/addSupplier",this.addSupplierForm);
        console.log(res);
        this.$message.success("用户创建成功！");
        this.getSupplierList();
        this.addyonghuDialogVisible = false;
      });
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
      this.$confirm("确认关闭？")
        .then(_ => {
          done();
        })
        .catch(_ => {});
    },
    deletebumen(supId) {
      this.$confirm("此操作将永久删除该职务, 是否继续?", "提示", {
        confirmButtonText: "确定",
        cancelButtonText: "取消",
        type: "warning"
      })
        .then(async () => {
          let param = new URLSearchParams();
          param.append("supId", supId);

          const { data: res } = await this.$http.post(
            "/jc/supplier/deleteSupplier",
            param
          );
          console.log(supId);
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