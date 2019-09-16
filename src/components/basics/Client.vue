<template>
  <div class="min1500">
    <!-- 面包屑导航区域 -->
    <el-breadcrumb separator-class="el-icon-arrow-right">
      <el-breadcrumb-item :to="{ path: '/welcome' }">首页</el-breadcrumb-item>
      <el-breadcrumb-item>基础资料</el-breadcrumb-item>
      <el-breadcrumb-item>客户管理</el-breadcrumb-item>
    </el-breadcrumb>
    <el-card>
      <el-row :gutter="20" class="row">
        <el-col :span="24">
          <el-row :gutter="20">
            <el-form :inline="true" class="demo-form-inline">
              <el-form-item label="客户名称：">
                <el-input placeholder="请输入客户名称"></el-input>
              </el-form-item>
              <el-form-item label="类型：">
                <el-input placeholder="请输入类型"></el-input>
              </el-form-item>
              <el-form-item label="联系人：">
                <el-input placeholder="请输入联系人"></el-input>
              </el-form-item>
              <el-form-item label="手机：">
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
          <el-table border stripe :data="tableData" @selection-change="handleSelectionChange">
            <el-table-column type="selection" width="55"></el-table-column>
            <el-table-column type="index"></el-table-column>
            <el-table-column prop="a" label="客户编码"></el-table-column>
            <el-table-column prop="b" label="客户名称"></el-table-column>
            <el-table-column prop="c" label="类型"></el-table-column>
            <el-table-column prop="d" label="联系人"></el-table-column>
            <el-table-column prop="e" label="手机"></el-table-column>
            <el-table-column prop="f" label="状态"></el-table-column>
            <el-table-column prop="g" label="创建人"></el-table-column>
            <el-table-column prop="h" label="创建时间"></el-table-column>
            <el-table-column label="状态" width="65px">
              <template>
                <el-switch active-color="#13ce66" inactive-color="#ff4949"></el-switch>
              </template>
            </el-table-column>
            <el-table-column label="操作" width="190px">
              <template>
                <el-button type="primary" icon="el-icon-edit" size="mini">修改</el-button>
                <el-button type="danger" icon="el-icon-delete" size="mini">删除</el-button>
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
      title="新增客户"
      :visible.sync="addyonghuDialogVisible"
      width="48%"
      :before-close="handleClose"
    >
      <el-form :label-position="labelPosition" label-width="120px">
        <el-row>
          <el-col :span="12">
            <el-form-item label="客户编码：">
              <el-input placeholder="客户编码"></el-input>
            </el-form-item>
            <el-form-item label="联系人：">
              <el-input placeholder="请输入联系人"></el-input>
            </el-form-item>
            <el-form-item label="邮箱：">
              <el-input placeholder="请输入联系邮箱"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="12">
            <el-form-item label="客户名称：">
              <el-input placeholder="请输入客户名称"></el-input>
            </el-form-item>
            <el-form-item label="手机：">
              <el-input placeholder="请输入手机"></el-input>
            </el-form-item>
            <el-form-item label="类型：">
              <el-select class="tiantou" placeholder="请选择类型">
                <el-option></el-option>
              </el-select>
            </el-form-item>
          </el-col>
        </el-row>
        <el-form-item label="联系地址：">
          <el-select placeholder="省级地区" class="hu">
            <el-option></el-option>
          </el-select>
          <el-select placeholder="市级地区" class="hu">
            <el-option></el-option>
          </el-select>
          <el-select placeholder="区级地区" class="hu">
            <el-option></el-option>
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
        <el-button @click="addyonghuDialogVisible = false">取 消</el-button>
        <el-button type="primary" @click="addyonghuDialogVisible = false">确 定</el-button>
      </span>
    </el-dialog>
    <el-dialog
      title="编辑客户"
      :visible.sync="edityonghuDialogVisible"
      width="48%"
      :before-close="handleClose"
    >
      <el-form :label-position="labelPosition" label-width="120px">
        <el-row>
          <el-col :span="12">
            <el-form-item label="客户编码：">
              <el-input placeholder="客户编码" v-model="tableData[0].a"></el-input>
            </el-form-item>
            <el-form-item label="联系人：">
              <el-input placeholder="请输入联系人" v-model="tableData[0].d"></el-input>
            </el-form-item>
            <el-form-item label="邮箱：">
              <el-input placeholder="请输入邮箱" v-model="tableData[0].i"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="12">
            <el-form-item label="客户名称：">
              <el-input placeholder="请输入客户名称" v-model="tableData[0].b"></el-input>
            </el-form-item>
            <el-form-item label="手机：">
              <el-input placeholder="请输入手机" v-model="tableData[0].e"></el-input>
            </el-form-item>
            <el-form-item label="类型：">
              <el-select class="tiantou" placeholder="请选择类型">
                <el-option></el-option>
              </el-select>
            </el-form-item>
          </el-col>
        </el-row>
        <el-form-item label="联系地址：">
          <el-select placeholder="省级地区" class="hu">
            <el-option></el-option>
          </el-select>
          <el-select placeholder="市级地区" class="hu">
            <el-option></el-option>
          </el-select>
          <el-select placeholder="区级地区" class="hu">
            <el-option></el-option>
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
export default {
  data() {
    return {
      labelPosition: "right",
      addyonghuDialogVisible: false,
      edityonghuDialogVisible: false,
      resetPassdialogVisible: false,
      currentPage1: 5,
      currentPage2: 5,
      currentPage3: 5,
      currentPage4: 4,
      selectedList: [],

      tableData: [
        {
          a: "GYSOO1",
          b: "祥子纸业",
          c: "原材料供应商",
          d: "祥子",
          e: "18859577302",
          f: "启用",
          g: "管理员",
          h: "2019-06-25 00:00",
          i: "53245454@qq.com",
          j: "",
          k: ""
        }
      ]
    };
  },
  created() {},
  methods: {
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
    deletebumen() {
      this.$confirm("此操作将永久删除该职务, 是否继续?", "提示", {
        confirmButtonText: "确定",
        cancelButtonText: "取消",
        type: "warning"
      })
        .then(() => {
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