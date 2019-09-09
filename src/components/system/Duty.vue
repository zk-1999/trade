<template>
    <div class="min1500">
       <!-- 面包屑导航区域 -->
      <el-breadcrumb separator-class="el-icon-arrow-right">
        <el-breadcrumb-item :to="{ path: '/welcome' }">首页</el-breadcrumb-item>
        <el-breadcrumb-item>系统管理</el-breadcrumb-item>
        <el-breadcrumb-item>职务设置</el-breadcrumb-item>
      </el-breadcrumb>
      <el-card class="quan">
        <div class="shu">
          <div class="togglr-button">全部部门</div>  
          <el-tree :data="data" :props="defaultProps" @node-click="handleNodeClick"></el-tree>
        </div>
      </el-card>
      <el-card class="min1300">
        <el-row :gutter="20" class="row">
          <el-col :span="24">
            <el-row :gutter="20">
                <span>&nbsp;&nbsp;&nbsp;职务名称：</span>
                <el-col :span="7">
                  <el-input placeholder="请输入职务名称" clearable  class="cor" >
                    <el-button slot="append" icon="el-icon-search"></el-button>
                  </el-input>
                </el-col>
                <el-col :span="3">
                  <el-button type="primary" >重置</el-button>
                </el-col>
            </el-row>
            <el-button type="success"  @click="addbumenDialogVisible = true">新增</el-button>
            <el-button type="warning" @click="editbumenDialogVisible= true">编辑</el-button> 
            <el-button type="danger"  @click="deletebumen">删除</el-button>
            <el-button type="info"  @click="rightDialogVisible= true">权限设置</el-button>
            <el-table border stripe  :data="tableData">
              <el-table-column type="selection" width="55"></el-table-column>
              <el-table-column type="index" width="50" ></el-table-column>              
              <el-table-column label="职务编号" property="date"></el-table-column>
              <el-table-column label="部门名称" property="name"></el-table-column>
              <el-table-column label="职务名称" property="address"></el-table-column>
              <el-table-column width="290px" label="备注" property="beizhu"></el-table-column>
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
          :total="400">
        </el-pagination>
      </el-card>
      <el-dialog
        title="新增职务"
        :visible.sync="addbumenDialogVisible"
        width="30%"
        :before-close="handleClose">
        <el-form :label-position="labelPosition" label-width="100px">
          <el-form-item label="职务编号："><el-input placeholder="请输入职务编号"></el-input></el-form-item>
          <el-form-item label="部门名称："><el-input placeholder="请输入部门名称"></el-input></el-form-item>
          <el-form-item label="职务名称："><el-input placeholder="请输入职务名称"></el-input></el-form-item>
          <el-form-item label="备注内容："><el-input type="textarea" :rows="2" placeholder="请输入备注内容"></el-input></el-form-item>
        </el-form>
        <span slot="footer" class="dialog-footer">
          <el-button @click="addbumenDialogVisible = false">取 消</el-button>
          <el-button type="primary" @click="addbumenDialogVisible = false">确 定</el-button>
        </span>
      </el-dialog>
      <el-dialog
        title="编辑职务"
        :visible.sync="editbumenDialogVisible"
        width="30%"
        :before-close="handleClose">
        <el-form :label-position="labelPosition" label-width="100px">
          <el-form-item label="职务编号："><el-input placeholder="请输入职务编号"></el-input></el-form-item>
          <el-form-item label="部门名称："><el-input placeholder="请输入部门名称"></el-input></el-form-item>
          <el-form-item label="职务名称："><el-input placeholder="请输入职务名称"></el-input></el-form-item>
          <el-form-item label="备注内容："><el-input type="textarea" :rows="2" placeholder="请输入备注内容"></el-input></el-form-item>
        </el-form>
        <span slot="footer" class="dialog-footer">
          <el-button @click="editbumenDialogVisible = false">取 消</el-button>
          <el-button type="primary" @click="editbumenDialogVisible = false">确 定</el-button>
        </span>
      </el-dialog>
      <el-dialog title="分配权限" :visible.sync="rightDialogVisible" width="50%" >
        <el-tree
          :data="rightList"
          show-checkbox
          node-key="id"
          default-expand-all
          :props="defaultPropss">
        </el-tree>
        <span slot="footer" class="dialog-footer">
            <el-button @click="rightDialogVisible = false">取 消</el-button>
            <el-button type="primary" @click="rightDialogVisible=false">确 定</el-button>
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
       currentPage1: 5,
       currentPage2: 5,
       currentPage3: 5,
       currentPage4: 4,
       tableData: [{
          date: '1001',
          name: '财务部',
          address: '财务总监',
          beizhu:'管理公司账务'
        }, {
          date: '1002',
          name: '财务部',
          address: '财务总监',
          beizhu:'管理公司账务'
        }, {
          date: '1003',
          name: '财务部',
          address: '财务总监',
          beizhu:'管理公司账务'
        }, {
          date: '1004',
          name: '财务部',
          address: '财务总监',
          beizhu:'管理公司账务'
        }, {
          date: '1005',
          name: '财务部',
          address: '财务总监',
          beizhu:'管理公司账务'
        }, {
          date: '1006',
          name: '财务部',
          address: '财务总监',
          beizhu:'管理公司账务'
        }, {
          date: '1007',
          name: '财务部',
          address: '财务总监',
          beizhu:'管理公司账务'
        }],
      addbumenDialogVisible: false,
      editbumenDialogVisible:false,
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
    .el-button{
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
</style>