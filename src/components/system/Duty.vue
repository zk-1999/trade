<template>
    <div class="min1500">
       <!-- 面包屑导航区域 -->
      <el-breadcrumb separator-class="el-icon-arrow-right">
        <el-breadcrumb-item :to="{ path: '/welcome' }">首页</el-breadcrumb-item>
        <el-breadcrumb-item>系统管理</el-breadcrumb-item>
        <el-breadcrumb-item>职务设置</el-breadcrumb-item>
      </el-breadcrumb>
      <el-card class="min1300">
        <el-row :gutter="20" class="row">
          <el-col :span="24">
            <el-row :gutter="20">
               <el-form :inline="true" class="demo-form-inline" :model="chaDutyForm" ref="chaDepartmentRef">
              <el-form-item label="职务名称：" prop="a">
                <el-input placeholder="请输入职务名称" v-model="chaDutyForm.roleName"></el-input>
              </el-form-item>
              <el-form-item>
                <el-button @click="getDutyList">查询</el-button>
                <el-button type="primary"  >重置</el-button>
              </el-form-item>
            </el-form>
            </el-row>
            <el-button type="success"  @click="addbumenDialogVisible = true">新增</el-button>
          <el-button type="danger" @click="selected" :disabled="selectedList.length == 0">批量删除</el-button>
            <el-button type="info"  @click="rightDialogVisible= true" :disabled="selectedList.length == 0">权限批量设置</el-button>
            <el-table border stripe  :data="DutyList" @selection-change="handleSelectionChange">
              <el-table-column type="selection" width="55"></el-table-column>
              <el-table-column type="index" width="50" ></el-table-column>              
              <el-table-column label="职务名称" prop="roleName" property="address"></el-table-column>
              <el-table-column prop="remark" label="备注" property="beizhu"></el-table-column>
              <el-table-column label="状态" width="65px">
                <template slot-scope="scope">
                  <el-switch
                  v-model="scope.row.status"
                  active-color="#13ce66"
                  inactive-color="#ff4949"
                  :active-value="1"
                  :inactive-value="0"
                  @change="userStateChanged(scope.row)"
                ></el-switch>
                </template>
              </el-table-column>
              <el-table-column label="操作" width="180">
                <template >
                   <el-tooltip effect="dark" content="修改" placement="top" :enterable="false">
                  <el-button size="mini" type="primary" icon="el-icon-edit"></el-button>
                  </el-tooltip>
                   <el-tooltip effect="dark" content="删除" placement="top" :enterable="false">
                <el-button size="mini" type="danger" icon="el-icon-delete"></el-button>
               </el-tooltip> 
               <el-tooltip effect="dark" content="权限分配" placement="top" :enterable="false">
                  <el-button size="mini" type="warning" icon="el-icon-setting"></el-button>
                </el-tooltip>
                </template>
              </el-table-column>
            </el-table>
          </el-col>
        </el-row>
        <el-pagination
          @size-change="handleSizeChange"
          @current-change="handleCurrentChange"
          :current-page="currentPage"
          :page-sizes="[3, 5, 10, 15]"
          :page-size="100"
          layout="total, sizes, prev, pager, next, jumper"
          :total="total">
        </el-pagination>
      </el-card>
      <el-dialog
        title="新增职务"
        :visible.sync="addbumenDialogVisible"
        width="30%"
        :before-close="handleClose">
        <el-form :label-position="labelPosition" label-width="100px"
        :model="addDutyForm"
        ref="addDutyRef"
        :rules="addDutyRules">
          <el-form-item label="职务名称：" prop="roleName"><el-input placeholder="请输入职务名称" v-model="addDutyForm.roleName"></el-input></el-form-item>
          <el-form-item label="备注内容：" prop="remark"><el-input type="textarea" :rows="2" placeholder="请输入备注内容" v-model="addDutyForm.remark"></el-input></el-form-item>
        </el-form>
        <span slot="footer" class="dialog-footer">
          <el-button @click="addbumenDialogVisible = false">取 消</el-button>
          <el-button type="primary" @click="addDuty">确 定</el-button>
        </span>
      </el-dialog>
      <!-- <el-dialog
        title="编辑职务"
        :visible.sync="editbumenDialogVisible"
        width="30%"
        :before-close="handleClose">
        <el-form :label-position="labelPosition" label-width="100px">
          <el-form-item label="部门名称："><el-input placeholder="请输入部门名称" v-model="table[0].a"></el-input></el-form-item>
          <el-form-item label="职务名称："><el-input placeholder="请输入职务名称" v-model="table[0].b"></el-input></el-form-item>
          <el-form-item label="备注内容："><el-input type="textarea" :rows="2" placeholder="请输入备注内容" v-model="table[0].c"></el-input></el-form-item>
        </el-form>
        <span slot="footer" class="dialog-footer">
          <el-button @click="editbumenDialogVisible = false">取 消</el-button>
          <el-button type="primary" @click="editbumenDialogVisible = false">确 定</el-button>
        </span>
      </el-dialog> -->
      <el-dialog title="分配权限" :visible.sync="rightDialogVisible" width="50%" >
        
        <hr>
        <el-row class="lei">
          <el-col :span="8">权限类别</el-col>
          <el-col :span="8">权限名称</el-col>
          <el-col :span="8">权限描述</el-col>
        </el-row>
        <el-row  v-for="(item1) in rightList" :key="item1.id" class="yi">
          <el-col :span="8">
            <el-checkbox>{{item1.authName}}</el-checkbox>
          </el-col>
          <el-col :span="16">
            <el-row v-for="(item2) in item1.children" :key="item2.id" class="er">
              <el-col :span="12">
                <el-checkbox>{{item2.authName}}</el-checkbox>
              </el-col>
              <el-col :span="12">
                备注
              </el-col>
            </el-row>
          </el-col>
        </el-row>
        <span slot="footer" class="dialog-footer">
            <el-button @click="rightDialogVisible = false">取 消</el-button>
            <el-button type="primary" @click="rightDialogVisible=false">确 定</el-button>
        </span>
      </el-dialog>
      <el-dialog title="提示" :visible.sync="delVisible" width="300px">
      <div class="del-dialog-cnt">删除不可恢复，是否确定删除？</div>
      <span slot="footer" class="dialog-footer">
          <el-button @click="delVisible = false">取 消</el-button>
          <el-button type="primary" @click="deleteRow" >确 定</el-button>
      </span>
    </el-dialog>
    </div>
</template>
<script>
export default {
  data () {
    return {
      rightList:[{"id":101,"authName":"商品管理","path":"goods","pid":0,"children":[{"id":104,"authName":"商品列表","path":"goods","pid":101,"children":[{"id":105,"authName":"添加商品","path":"goods","pid":"104,101"},{"id":116,"authName":"商品修改","path":"goods","pid":"104,101"},{"id":117,"authName":"商品删除","path":"goods","pid":"104,101"},{"id":150,"authName":"更新商品图片","path":"goods","pid":"104,101"},{"id":151,"authName":"更新商品属性","path":"goods","pid":"104,101"},{"id":152,"authName":"更新商品状态","path":"goods","pid":"104,101"},{"id":153,"authName":"获取商品详情","path":"goods","pid":"104,101"}]},{"id":115,"authName":"分类参数","path":"params","pid":101,"children":[{"id":142,"authName":"获取参数列表","path":"categories","pid":"115,101"},{"id":143,"authName":"创建商品参数","path":"categories","pid":"115,101"},{"id":144,"authName":"删除商品参数","path":"categories","pid":"115,101"}]},{"id":121,"authName":"商品分类","path":"categories","pid":101,"children":[{"id":122,"authName":"添加分类","path":"categories","pid":"121,101"},{"id":123,"authName":"删除分类","path":"categories","pid":"121,101"},{"id":149,"authName":"获取分类详情","path":"categories","pid":"121,101"}]}]},{"id":102,"authName":"订单管理","path":"orders","pid":0,"children":[{"id":107,"authName":"订单列表","path":"orders","pid":102,"children":[{"id":109,"authName":"添加订单","path":"orders","pid":"107,102"},{"id":154,"authName":"订单更新","path":"orders","pid":"107,102"},{"id":155,"authName":"获取订单详情","path":"orders","pid":"107,102"}]}]},{"id":103,"authName":"权限管理","path":"rights","pid":0,"children":[{"id":111,"authName":"角色列表","path":"roles","pid":103,"children":[{"id":129,"authName":"添加角色","path":"roles","pid":"111,103"},{"id":130,"authName":"删除角色","path":"roles","pid":"111,103"},{"id":134,"authName":"角色授权","path":"roles","pid":"111,103"},{"id":135,"authName":"取消角色授权","path":"roles","pid":"111,103"},{"id":138,"authName":"获取角色列表","path":"roles","pid":"111,103"},{"id":139,"authName":"获取角色详情","path":"roles","pid":"111,103"},{"id":140,"authName":"更新角色信息","path":"roles","pid":"111,103"},{"id":141,"authName":"更新角色权限","path":"roles","pid":"111,103"}]},{"id":112,"authName":"权限列表","path":"rights","pid":103,"children":[{"id":147,"authName":"查看权限","path":"rights","pid":"112,103"}]}]},{"id":125,"authName":"用户管理","path":"users","pid":0,"children":[{"id":110,"authName":"用户列表","path":"users","pid":125,"children":[{"id":131,"authName":"添加用户","path":"users","pid":"110,125"},{"id":132,"authName":"删除用户","path":"users","pid":"110,125"},{"id":133,"authName":"更新用户","path":"users","pid":"110,125"},{"id":136,"authName":"获取用户详情","path":"users","pid":"110,125"},{"id":137,"authName":"分配用户角色","path":"users","pid":"110,125"},{"id":159,"authName":"设置管理状态","path":"users","pid":"110,125"}]}]},{"id":145,"authName":"数据统计","path":"reports","pid":0,"children":[{"id":146,"authName":"数据报表","path":"reports","pid":145,"children":[{"id":148,"authName":"查看数据","path":"reports","pid":"146,145"}]}]}],
      defaultPropss: {
        children: 'children',
        label: 'authName'
       },
      labelPosition: 'right',
      rightDialogVisible:false,
      addbumenDialogVisible: false,
      editbumenDialogVisible:false,
      delVisible:false,
      delarr:'',
      currentPage: 0,
      total:0,
      chaDutyForm:{
        roleName:'',
        pageCode: 1, //当前页
        pageSize: 3,//每页显示的记录数
      },
      DutyList:[],
      selectedList: [],
      addDutyForm:{
        roleName:'',
        remark:'',
      },
      addDutyRules: {
          roleName:[
          { required: true, message: '请输入用户名', trigger: 'blur' },
          { min: 3, max: 10, message: '长度在 3 到 10 个字符', trigger: 'blur' }
          ],},
    }
  },
  created () {  
    this.getDutyList();
  },
  methods:{
    async getDutyList() {
      const { data: res } = await this.$http.post("sys/role/list",{params:this.chaDutyForm});
      console.log(res);
      
      this.total=res.body.total;
      this.DutyList = res.body.rows;
    },
    addDuty() {
      this.$refs.addDutyRef.validate(async valid => {
        if (!valid) return;    
        const { data: res } = await this.$http.post("sys/role/save",{params:this.addDutyForm});
        this.$message.success("用户创建成功！");
        this.getDutyList();
        this.addbumenDialogVisible = false;
      });
    },
    selected(){
      this.delarr=[];
      this.delVisible = true;
      for (let i = 0; i < this.selectedList.length; i++) {
        this.delarr+=this.selectedList[i].deptId+','
      }
      console.log(this.delarr);
    },
    async deleteRow(){
      let param = new URLSearchParams();
      param.append("deptIds", this.delarr);
         const {data:res} = await this.$http.post('sys/dept/batchRemove',param);
         this.delVisible = false;
         this.getDepartmentList();
      },
    handleSizeChange(val) {
      this.chaDutyForm.pageSize=val;
      console.log(`每页 ${val} 条`);
      this.getDepartmentList();
    },
    handleCurrentChange(val) {
      this.chaDutyForm.pageCode=val;
      this.currentPage=val;
      console.log(`当前页: ${val}`);
      this.getDepartmentList();
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
    .el-tag{
        margin: 7px;
    }
    .el-row{
        align-items: center;
        display: flex;
    }
    .el-table{
        margin-top: 15px;
    }

    .quan{
      float: left;
      margin-right: 20px;
      // width: 220px !important;
      // min-width: 220px;
    }
    .el-card{
      height: 650px;
    }
    .togglr-button{
      width: 180px;
      height: 30px;
      background: #eee;
      text-align: center;
      line-height: 30px;
    }
    .el-pagination{
        margin-top: 30px;
    }
    .yi{
      border-bottom: 1px solid #999;
      text-align: center;
      margin-top: 20px;
      margin-bottom: 20px;
    }
    .er{
      margin-top: 20px;
      margin-bottom: 20px;
    }
    .lei{
      text-align: center;
      background: #999;
      padding: 5px;
    }
    .chongzhi{
      margin-top: 0px;
    }
</style>