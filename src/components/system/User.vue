<template>
    <div class="min1500">
       <!-- 面包屑导航区域 -->
      <el-breadcrumb separator-class="el-icon-arrow-right">
        <el-breadcrumb-item :to="{ path: '/welcome' }">首页</el-breadcrumb-item>
        <el-breadcrumb-item>系统管理</el-breadcrumb-item>
        <el-breadcrumb-item>用户管理</el-breadcrumb-item>
      </el-breadcrumb>
      <el-card class="quan">
        <div class="shu">
          <div class="togglr-button">全部部门</div>  
          <el-tree :data="data" :props="defaultProps" @node-click="handleNodeClick"></el-tree>
        </div>
      </el-card>
      <el-card>
        <el-row :gutter="20" class="row">
          <el-col :span="24">
             <el-row :gutter="20">
                <el-form :inline="true" class="demo-form-inline">
                    <el-form-item label="姓名：">
                    <el-input placeholder="请输入姓名"></el-input>
                    </el-form-item>
                    <el-form-item label="工号：">
                    <el-input placeholder="请输入工号"></el-input>
                    </el-form-item>
                    <el-form-item label="出生日期：">
                    <el-input placeholder="请输入出生日期"></el-input>
                    </el-form-item>
                    <el-form-item label="入职离职日期：">
                    <el-input placeholder="请输入入职离职日期"></el-input>
                    </el-form-item>
                    <el-form-item>
                        <el-button >查询</el-button>
                        <el-button type="primary">重置</el-button>
                    </el-form-item>
                </el-form>
        </el-row>
          <el-button type="success" @click="addyonghuDialogVisible = true">新增</el-button>
          <el-button type="danger" @click="resetPassdialogVisible=true" :disabled="selectedList.length == 0">密码批量重置</el-button>
           <el-button type="warning" @click="editbumenDialogVisible= true" :disabled="selectedList.length == 0">批量启用</el-button>
           <el-button type="warning" @click="editbumenDialogVisible= true" :disabled="selectedList.length == 0">批量禁用</el-button>

         <el-button type="danger" @click="deletebumen" :disabled="selectedList.length == 0">批量删除</el-button>
          <el-table border stripe :data="table" @selection-change="handleSelectionChange">
            <el-table-column type="selection" width="55"></el-table-column>
            <el-table-column type="index"></el-table-column>
            <!-- <el-table-column prop="roleName" label="头像"></el-table-column> -->
            <el-table-column prop="a" label="姓名"></el-table-column>
            <el-table-column prop="b" label="登录账号"></el-table-column>
            <el-table-column prop="c" label="手机号码" width="115px"></el-table-column>
            <el-table-column prop="d" label="部门"></el-table-column>
            <el-table-column prop="e" label="职务"></el-table-column>
            <el-table-column prop="f" label="分销业务"></el-table-column>
            <el-table-column prop="g" label="性别"></el-table-column>
            <el-table-column prop="h" label="工号"></el-table-column>
            <el-table-column prop="i" label="地区"></el-table-column>
            <el-table-column prop="j" label="备注"></el-table-column>
             <el-table-column label="状态" width="65px">
              <template >
                <el-switch active-color="#13ce66" inactive-color="#ff4949"></el-switch>
              </template>
            </el-table-column>
            <el-table-column  label="操作" width="190px">
              <template slot-scope="scope">
                  <el-button type="primary" icon="el-icon-edit"  size="mini">修改</el-button>
                  <el-button type="danger" icon="el-icon-delete" size="mini"  @click="removeGoods(scope.row.goods_id)">删除</el-button>
              </template>
            </el-table-column>
          </el-table></el-col>
        </el-row>
      </el-card>
      <el-dialog
        title="新增用户"
        :visible.sync="addyonghuDialogVisible"
        width="48%"
        :before-close="handleClose">
        <el-form :label-position="labelPosition" label-width="120px">
          <el-row>
            <el-col :span="12">
              <el-form-item label="姓名："><el-input placeholder="请输入姓名"></el-input></el-form-item>
              <el-form-item label="登录账号："><el-input placeholder="请输入登录账号"></el-input></el-form-item>
              <el-form-item label="部门：">
                <el-select class="tiantou" placeholder="请选择部门">
                  <el-option></el-option>
                </el-select>
              </el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item label="手机号："><el-input placeholder="请输入手机"></el-input></el-form-item>
              <el-form-item label="工号："><el-input placeholder="工号"></el-input></el-form-item>
              <el-form-item label="职务：">
                <el-select class="tiantou" placeholder="请选择职务">
                  <el-option></el-option>
                 </el-select>
              </el-form-item>
            </el-col>
          </el-row>
          <hr>
          <div class="xiang">详细信息</div>
          <el-form-item label="性别：">
            <el-radio-group>
              <el-radio label="男"></el-radio>
              <el-radio label="女"></el-radio>
            </el-radio-group>
          </el-form-item>
          <el-form-item label="岗位：">
            <el-radio-group>
              <el-radio label="在岗"></el-radio>
              <el-radio label="未在岗"></el-radio>
            </el-radio-group>
          </el-form-item>
          <el-form-item label="婚姻：">
            <el-radio-group>
              <el-radio label="已婚"></el-radio>
              <el-radio label="未婚"></el-radio>
              <el-radio label="离异"></el-radio>
              <el-radio label="丧偶"></el-radio>
            </el-radio-group>
          </el-form-item>
          <el-form-item label="民族："><el-input placeholder="请输入民族" class="xiang"></el-input></el-form-item>
          <el-form-item label="出生日期："><el-input placeholder="请输入出生日期" class="xiang"></el-input></el-form-item>
          <el-form-item label="身份证号码："><el-input placeholder="请输入身份证号码" class="xiang"></el-input></el-form-item>
          <el-form-item label="户籍：">
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
          <el-form-item label="详细地址："><el-input placeholder="请输入详细地址" class="xiang"></el-input></el-form-item>          
          <el-form-item label="紧急联系人："><el-input placeholder="请输入紧急联系人" class="xiang"></el-input></el-form-item>
          <el-form-item label="银行卡号："><el-input placeholder="请输入银行卡号" class="xiang"></el-input></el-form-item>
          <el-form-item label="通讯地址：">
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
          <el-form-item label="通讯详细地址："><el-input placeholder="请输入通讯地址" class="xiang"></el-input></el-form-item>
          <el-form-item label="入职时间："><el-input placeholder="请输入入职时间" class="xiang"></el-input></el-form-item>
          <el-form-item label="离职时间："><el-input placeholder="请输入离职时间" class="xiang"></el-input></el-form-item>
        </el-form>
        <span slot="footer" class="dialog-footer">
          <el-button @click="addyonghuDialogVisible = false">取 消</el-button>
          <el-button type="primary" @click="addyonghuDialogVisible = false">确 定</el-button>
        </span>
      </el-dialog>
      <el-dialog
        title="编辑用户"
        :visible.sync="edityonghuDialogVisible"
        width="48%"
        :before-close="handleClose">
        <el-form :label-position="labelPosition" label-width="120px">
          <el-row>
            <el-col :span="12">
              <el-form-item label="姓名："><el-input placeholder="请输入姓名" v-model="table[0].a"></el-input></el-form-item>
              <el-form-item label="登录账号："><el-input placeholder="请输入登录账号" v-model="table[0].b"></el-input></el-form-item>
              <el-form-item label="部门：">
                <el-select class="tiantou" placeholder="请选择部门">
                  <el-option></el-option>
                </el-select>
              </el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item label="手机号："><el-input placeholder="请输入手机"  v-model="table[0].c"></el-input></el-form-item>
              <el-form-item label="工号："><el-input placeholder="工号" v-model="table[0].h"></el-input></el-form-item>
              <el-form-item label="职务：">
                <el-select class="tiantou" placeholder="请选择职务">
                  <el-option></el-option>
                 </el-select>
              </el-form-item>
            </el-col>
          </el-row>
          <hr>
          <div class="xiang">详细信息</div>
          <el-form-item label="性别：">
            <el-radio-group>
              <el-radio label="男"></el-radio>
              <el-radio label="女"></el-radio>
            </el-radio-group>
          </el-form-item>
          <el-form-item label="岗位：">
            <el-radio-group>
              <el-radio label="在岗"></el-radio>
              <el-radio label="未在岗"></el-radio>
            </el-radio-group>
          </el-form-item>
          <el-form-item label="婚姻：">
            <el-radio-group>
              <el-radio label="已婚"></el-radio>
              <el-radio label="未婚"></el-radio>
              <el-radio label="离异"></el-radio>
              <el-radio label="丧偶"></el-radio>
            </el-radio-group>
          </el-form-item>
          <el-form-item label="民族："><el-input placeholder="请输入民族" class="xiang"></el-input></el-form-item>
          <el-form-item label="出生日期："><el-input placeholder="请输入出生日期" class="xiang"></el-input></el-form-item>
          <el-form-item label="身份证号码："><el-input placeholder="请输入身份证号码" class="xiang"></el-input></el-form-item>
          <el-form-item label="户籍：">
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
          <el-form-item label="详细地址："><el-input placeholder="请输入详细地址" class="xiang"></el-input></el-form-item>          
          <el-form-item label="紧急联系人："><el-input placeholder="请输入紧急联系人" class="xiang"></el-input></el-form-item>
          <el-form-item label="银行卡号："><el-input placeholder="请输入银行卡号" class="xiang"></el-input></el-form-item>
          <el-form-item label="通讯地址：">
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
          <el-form-item label="通讯详细地址："><el-input placeholder="请输入通讯地址" class="xiang"></el-input></el-form-item>
          <el-form-item label="入职时间："><el-input placeholder="请输入入职时间" class="xiang"></el-input></el-form-item>
          <el-form-item label="离职时间："><el-input placeholder="请输入离职时间" class="xiang"></el-input></el-form-item>
        </el-form>
        <span slot="footer" class="dialog-footer">
          <el-button @click="edityonghuDialogVisible = false">取 消</el-button>
          <el-button type="primary" @click="edityonghuDialogVisible = false">确 定</el-button>
        </span>
      </el-dialog>
      <el-dialog
        title="密码重置"
        :visible.sync="resetPassdialogVisible"
        width="35%"
        :before-close="handleClose">
        <el-form :label-position="labelPosition" label-width="100px">
          <el-form-item label="登录账号："><el-input placeholder="请输入登录账号"></el-input></el-form-item>
          <el-form-item label="旧密码："><el-input placeholder="请输入旧密码"></el-input></el-form-item>
          <el-form-item label="新密码："><el-input placeholder="请输入新密码"></el-input></el-form-item>
          <el-form-item label="确认新密码："><el-input placeholder="请输入确认新密码"></el-input></el-form-item>
        </el-form>
        <span slot="footer" class="dialog-footer">
          <el-button @click="resetPassdialogVisible = false">取 消</el-button>
          <el-button type="primary" @click="resetPassdialogVisible = false">保 存</el-button>
        </span>
      </el-dialog>
    </div>
</template>
<script>
export default {
  data () {
    return {
      selectedList: [],
      labelPosition: 'right',
      addyonghuDialogVisible: false,
      edityonghuDialogVisible:false,
      resetPassdialogVisible:false,
      table: [{
          a: '张三',
          b: 'zhangsan',
          c: '18354682635',
          d:'采购部门',
          e:'主管',
          f:'未知',
          g:'男',
          h:'0003',
          i:'杭州',
          j:'备注',
          k:''
        }],
      data: [{
          label: '一级 1',
          children: [{
            label: '二级 1-1',
            children: [{
              label: '三级 1-1-1'
            }]
          }]
        }, {
          label: '一级 2',
          children: [{
            label: '二级 2-1',
            children: [{
              label: '三级 2-1-1'
            }]
          }, {
            label: '二级 2-2',
            children: [{
              label: '三级 2-2-1'
            }]
          }]
        }, {
          label: '一级 3',
          children: [{
            label: '二级 3-1',
            children: [{
              label: '三级 3-1-1'
            }]
          }, {
            label: '二级 3-2',
            children: [{
              label: '三级 3-2-1'
            }]
          }]
        }],
        defaultProps: {
          children: 'children',
          label: 'label'
        }
    }
  },
  created () {
  },
  methods:{
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
     },
       handleSelectionChange(val) {
      console.log(val);
      this.selectedList = val;
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
    .togglr-button{
      width: 180px;
      height: 30px;
      background: #eee;
      padding-right: -10px;
      text-align: center;
      line-height: 30px;
    }
    .demo-form-inline .el-input{
      width: 180px;
    }
    .el-select{
      width: 225px;
    }
    .quan{
      float: left;
      margin-right: 20px;
    }
    .el-card{
      height: 650px;
    }
    .xiang{
      width: 400px;
    }
    .hu{
      width: 133px;
    }
</style>