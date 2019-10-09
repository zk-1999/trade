<template>
    <el-container class="home-container">
        <el-header>
            <div>
                <img src="../assets/log.png" alt="login">
                <span>贸普实业ERP管理系统</span>
            </div>
           <div class="tubiao"> 
               <div class="im"><img src="../assets/img/yong.jpg" alt=""></div>
               <div class="yong">你好，{{username}}</div>
               <el-badge  :value="3" class="item tuituxin"><el-button size="small" type="success" circle icon="el-icon-chat-line-round"></el-button></el-badge>
               <el-button class="tuituxin" type="warning" icon="el-icon-setting" size="small" circle @click="shezhidialogVisible=true"></el-button>
               <el-button type="info" @click="logout" size="small" class="tuituxin">退出</el-button>
            </div>
        </el-header>
        <el-container>
            <el-aside :width="isCollapse ? '64px' : '200px'">
                <div class="togglr-button" @click="toggleCollapse">|||</div>
                <el-menu background-color="#001529" text-color="#fff" active-text-color="#409eff" :unique-opened="true" :collapse="isCollapse" :collapse-transition="false"
                :router="true" :default-active="activePath">
                    <!-- 一级菜单 -->
                <el-submenu :index="item.id+''" v-for="item in menuList" :key="item.id">
                <!-- 一级菜单的模板区域 -->
                    <template slot="title">
                        <!-- 图标 -->
                    <i :class="iconsObj[item.id]"></i>
                    <!-- 文本 -->
                    <span>{{item.authName}}</span>
                    </template>
                    <!-- 二级菜单的模板区域 -->
                    <el-menu-item :index="'/'+subItem.path" v-for="subItem in item.children" :key="subItem.id" @click="saveNavState('/'+subItem.path)">
                         <!-- 图标 -->
                    <i class="el-icon-menu"></i>
                    <!-- 文本 -->
                    <span>{{subItem  .authName}}</span>
                    </el-menu-item>
                </el-submenu>
                </el-menu>
            </el-aside>
            <el-main><router-view></router-view></el-main>
        </el-container>
        <el-dialog
        title="基本设置"
        :visible.sync="shezhidialogVisible"
        width="40%"
        :before-close="handleClose">
        <div class="ti">
            <el-form :label-position="labelPosition" label-width="100px">
                <el-form-item class="tupian">
                    <el-upload
                        class="avatar-uploader"
                        action="https://jsonplaceholder.typicode.com/posts/"
                        :show-file-list="false"
                        :on-success="handleAvatarSuccess"
                        :before-upload="beforeAvatarUpload">
                        <img v-if="imageUrl" :src="imageUrl" class="avatar">
                        <i v-else class="el-icon-plus avatar-uploader-icon"></i>
                    </el-upload>
                </el-form-item>
                <el-form-item class="tian" label="用户名:"><el-input  placeholder="请输入用户名"></el-input></el-form-item>
                <el-form-item class="tian" label="手机号:"><el-input  placeholder="请输入手机号"></el-input></el-form-item>
                <el-form-item class="tian" label="邮箱:"><el-input  placeholder="请输入邮箱"></el-input></el-form-item>
                <el-form-item class="tian" label="旧密码:"><el-input  placeholder="请输入旧密码"></el-input></el-form-item>
                <el-form-item class="tian" label="新密码:"><el-input  placeholder="请输入新密码"></el-input></el-form-item>
                <el-form-item class="tian" label="确认新密码:"><el-input  placeholder="请输入确认新密码"></el-input></el-form-item>
            </el-form>
        </div>
        <span slot="footer" class="dialog-footer">
            <el-button @click="shezhidialogVisible = false">取 消</el-button>
            <el-button type="primary" @click="shezhidialogVisible = false">确 定</el-button>
        </span>
        </el-dialog>
    </el-container>
</template>
<script>
export default {
    data () {
        return {
            imageUrl: '',
            labelPosition: 'right',
            shezhidialogVisible : false,
            menuList:[{"id":125,"authName":"基础资料","path":"basics","children":[{"id":110,"authName":"供应商管理","path":"supplier","children":[],"order":null},{"id":111,"authName":"客户管理","path":"client","children":[],"order":null},{"id":112,"authName":"供应商商品管理","path":"merchandise","children":[],"order":null},{"id":113,"authName":"生产商品管理","path":"production","children":[],"order":null},{"id":114,"authName":"产品设计稿维护","path":"product","children":[],"order":null},{"id":115,"authName":"印刷参数","path":"printing","children":[],"order":null},{"id":116,"authName":"基础数据维护","path":"maintenance","children":[],"order":null}],"order":1},{"id":103,"authName":"系统管理","path":"rights","children":[{"id":111,"authName":"部门设置","path":"department","children":[],"order":null},{"id":112,"authName":"职务设置","path":"duty","children":[],"order":null},{"id":113,"authName":"用户管理","path":"user","children":[],"order":null},{"id":114,"authName":"菜单管理","path":"menu","children":[],"order":null},{"id":115,"authName":"系统日志","path":"journal","children":[],"order":null}],"order":2},{"id":101,"authName":"进货管理","path":"goods","children":[],"order":3},{"id":102,"authName":"销售管理","path":"orders","children":[],"order":4},{"id":145,"authName":"生产管理","path":"reports","children":[],"order":5}],
            iconsObj:{
                '125':'iconfont icon-user',
                '103':'iconfont icon-tijikongjian',
                '101':'iconfont icon-shangpin',
                '102':'iconfont icon-danju',
                '145':'iconfont icon-baobiao'
            },
            //是否折叠
            isCollapse:false,
            //被激活的链接地址
            activePath:'',
            username:'',
        };
    },
    created () {
        // this.getMenuList(),
        this.activePath=window.sessionStorage.getItem('activePath')
        // this.username=window.sessionStorage.getItem('username')
        // console.log(username);
        this.getCookie();
    },
    methods:{
      
        handleAvatarSuccess(res, file) {
        this.imageUrl = URL.createObjectURL(file.raw);
      },
      beforeAvatarUpload(file) {
        const isJPG = file.type === 'image/jpeg';
        const isLt2M = file.size / 1024 / 1024 < 2;

        if (!isJPG) {
          this.$message.error('上传头像图片只能是 JPG 格式!');
        }
        if (!isLt2M) {
          this.$message.error('上传头像图片大小不能超过 2MB!');
        }
        return isJPG && isLt2M;
      },
        logout(){
            window.sessionStorage.clear();
            this.$router.push('/login');
        },
        async getMenuList(){
            // this.$http.get('menus').then((res) => {
            //     console.log(res);
            //     this.menuList = res;
            // }).catch(err => err)
        //  const {data:res} = await this.$http.get('menus');
        //   if(res.meta.status!==200) return this.$message.error(res.meta.msg)
        //   this.menuList=res.data
        },
        getCookie: function() {
            
            
          if (document.cookie.length > 0) {
              var arr = document.cookie.split('; '); //这里显示的格式需要切割一下自己可输出看下
              for (var i = 0; i < arr.length; i++) {
                  var arr2 = arr[i].split('='); //再次切割
                  //判断查找相对应的值
                  
                  if (arr2[0] == 'userName') {
                    //  console.log(arr2[1])
                      this.username = arr2[1]; //保存到保存数据的地方
                  }
              }
          }
      },
        //点击按钮，切换菜单的折叠与展开
        toggleCollapse(){
            this.isCollapse=!this.isCollapse;
        },

        //保存链接的激活状态
        saveNavState(activePath){
        window.sessionStorage.setItem('activePath',activePath);
        this.activePath=activePath
        },
        handleClose(done) {
        this.$confirm('确认关闭？')
          .then(_ => {
            done();
          })
          .catch(_ => {});
    },
    }
}
</script>
<style lang='less' scoped>
    .home-container{
        height: 100%;
    }
    .el-header{
        background-color: #001529;
        display:flex;
        justify-content:space-between;
        padding-left: 0;
        align-items:center;
        color: #fff;
        font-size: 20px;
        > div{
            display: flex;
            align-items:center;
            span{
                margin-left: 15px;
            }
        }
    }
    .el-aside{
        background-color: #001529;
        .el-menu{
            border-right: none;
        }
    }
    .el-main{
        background-color: #eaedf1;
    }
    .iconfont{
        margin-right: 10px;
    }
    .togglr-button{
        background-color: #4a5064;
        font-size: 10px;
        line-height: 24px;
        color: #fff;
        text-align: center;
        letter-spacing: 0.2em;
        cursor: pointer;
    }
    .el-header img{
        width: 61px;
        height: 56px;
    }
    .tubiao{
        // margin-top: 15px;
        .im{
            // width: 45px;
            height: 45px;
            img {
                width: 30px;
                height: 30px;
                border-radius: 50%;
                margin-top: 8px;
            }
        }
        .yong{
            // width: 120px;
            height: 35px;
            padding-top: 10px;
            font-size: 18px;
            padding-left: 15px;
        }
        .el-button{
            margin-left: 15px;
        }
    }
    .ti{
        width: 430px;
      .tian{
            margin-left: 20px;
        .el-input{
            width: 320px;
        }
      }
      .el-button{
          margin-left: 140px;
          margin-top: 10px;
      }
    }
   .avatar-uploader .el-upload {
    border: 1px dashed #d9d9d9;
    border-radius: 6px;
    cursor: pointer;
    position: relative;
    overflow: hidden;
  }
  .avatar-uploader .el-upload:hover {
    border-color: #409EFF;
  }
  .avatar-uploader-icon {
    font-size: 28px;
    color: #8c939d;
    width: 178px;
    height: 178px;
    line-height: 178px;
    text-align: center;
  }
  .avatar {
    width: 178px;
    height: 178px;
    display: block;
  }
  
</style>