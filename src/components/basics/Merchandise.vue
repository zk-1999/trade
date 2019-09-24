<template>
  <div class="min1500">
    <!-- 面包屑导航区域 -->
    <el-breadcrumb separator-class="el-icon-arrow-right">
      <el-breadcrumb-item :to="{ path: '/welcome' }">首页</el-breadcrumb-item>
      <el-breadcrumb-item>基础资料</el-breadcrumb-item>
      <el-breadcrumb-item>供应商商品管理</el-breadcrumb-item>
    </el-breadcrumb>
    <el-card>
      <el-tabs @tab-click="handleClick" type="border-card">
    <el-tab-pane label="纸张" >
      <el-form :inline="true" class="demo-form-inline" :model="chamerchandiseForm" ref="chamerchandiseRef">
              <el-form-item label="供应商名称：" prop="supName">
                <el-select v-model="chamerchandiseForm.supName" placeholder="请选择">
                  <el-option
                    v-for="item in chamerchandiseForm1"
                    :key="item.suppliergoolsId"
                    :label="item.supName"
                    :value="item.supName">
                  </el-option>
                </el-select>
              </el-form-item>
              <el-form-item label="商品小类型：" prop="supgoolssmallType">
                <el-select v-model="chamerchandiseForm.supgoolssmallType" placeholder="请选择">
                  <el-option
                    v-for="item in chamerchandiseForm1"
                    :key="item.suppliergoolsId"
                    :label="item.supgoolssmallType"
                    :value="item.supgoolssmallType">
                  </el-option>
                </el-select>
              </el-form-item>
              <el-form-item>
                <el-button @click="getMerchandiseList5">查询</el-button>
                <el-button type="primary" @click="chaMerchandiseResetForm">重置</el-button>
              </el-form-item>
            </el-form>
          <el-button type="success" @click="addyonghuDialogVisible = true">新增</el-button>
          <el-button
            type="warning"
            @click="selectedqi"
            :disabled="selectedList.length == 0"
          >批量启用/禁用</el-button>
          <el-button type="danger" @click="selected" :disabled="selectedList.length == 0">批量删除</el-button>
      <el-table :data="merchandiseList" border @selection-change="handleSelectionChange">
            <el-table-column type="selection" width="35" align="center"></el-table-column>
            <el-table-column type="index" width="35" fixed align="center"></el-table-column>
            <el-table-column prop="supId" label="供应商编码"  align="center"></el-table-column>
            <el-table-column prop="supName" label="供应商名称"  align="center"></el-table-column>
            <el-table-column prop="supgoolsBigType" label="商品大类型"  align="center"></el-table-column>
            <el-table-column prop="supgoolsId" label="商品编号" align="center"></el-table-column>
            <el-table-column prop="supgoolssmallType" label="商品小类型"  align="center"></el-table-column>
            <el-table-column prop="supgoolCoated" label="淋膜类型"  align="center"></el-table-column>
            <el-table-column prop="supgoolsBrand" label="品牌" align="center"></el-table-column>
            <el-table-column prop="supgoolsWeight" label="克重" align="center"></el-table-column>
            <el-table-column prop="supgoolsWidths" label="门幅" align="center"></el-table-column>
            <el-table-column label="状态" width="65px" align="center">
              <template slot-scope="scope">
                <el-switch
                  v-model="scope.row.supgoolsState"
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
                <el-button type="primary" icon="el-icon-edit" size="mini" @click="showMerchandise(scope.row.suppliergoolsId)">修改</el-button>
                <el-button
                  type="danger"
                  icon="el-icon-delete"
                  @click="deletebumen(scope.row.suppliergoolsId)"
                  size="mini"
                >删除</el-button>
              </template>
            </el-table-column>
          </el-table>
    </el-tab-pane>
    <el-tab-pane label="纸箱" >
      <el-form :inline="true" class="demo-form-inline" :model="chamerchandiseForm" ref="chamerchandiseRef">
              <el-form-item label="供应商名称：" prop="supName">
                <el-select v-model="chamerchandiseForm.supName" placeholder="请选择">
                  <el-option
                    v-for="item in chamerchandiseForm1"
                    :key="item.suppliergoolsId"
                    :label="item.supName"
                    :value="item.supName">
                  </el-option>
                </el-select>
              </el-form-item>
              <el-form-item label="商品小类型：" prop="supgoolssmallType">
                <el-select v-model="chamerchandiseForm.supgoolssmallType" placeholder="请选择">
                  <el-option
                    v-for="item in chamerchandiseForm1"
                    :key="item.suppliergoolsId"
                    :label="item.supgoolssmallType"
                    :value="item.supgoolssmallType">
                  </el-option>
                </el-select>
              </el-form-item>
              <el-form-item>
                <el-button @click="getMerchandiseList6">查询</el-button>
                <el-button type="primary" @click="chaMerchandiseResetForm">重置</el-button>
              </el-form-item>
            </el-form>
          <el-button type="success" @click="addyonghuDialogVisible = true">新增</el-button>
          <el-button
            type="warning"
            @click="selectedqi"
            :disabled="selectedList.length == 0"
          >批量启用/禁用</el-button>
          <el-button type="danger" @click="selected" :disabled="selectedList.length == 0">批量删除</el-button>
      <el-table :data="merchandiseList" border @selection-change="handleSelectionChange">
            <el-table-column type="selection" width="35" align="center"></el-table-column>
            <el-table-column type="index" width="35" fixed align="center"></el-table-column>
            <el-table-column prop="supId" label="供应商编码" align="center"></el-table-column>
            <el-table-column prop="supName" label="供应商名称" align="center"></el-table-column>
            <el-table-column prop="supgoolsBigType" label="商品大类型" align="center"></el-table-column>
            <el-table-column prop="supgoolsId" label="商品编号" align="center"></el-table-column>
            <el-table-column prop="supgoolssmallType" label="商品小类型" align="center"></el-table-column>
            <el-table-column prop="supgoolsWeight" label="克重" align="center"></el-table-column>
            <el-table-column label="状态" width="65px" align="center">
              <template slot-scope="scope">
                <el-switch
                  v-model="scope.row.supgoolsState"
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
                <el-button type="primary" icon="el-icon-edit" size="mini" @click="showMerchandise(scope.row.suppliergoolsId)">修改</el-button>
                <el-button
                  type="danger"
                  icon="el-icon-delete"
                  @click="deletebumen(scope.row.suppliergoolsId)"
                  size="mini"
                >删除</el-button>
              </template>
            </el-table-column>
          </el-table>
    </el-tab-pane>
    <el-tab-pane label="袋子" >
      <el-form :inline="true" class="demo-form-inline" :model="chamerchandiseForm" ref="chamerchandiseRef">
              <el-form-item label="供应商名称：" prop="supName">
                <el-select v-model="chamerchandiseForm.supName" placeholder="请选择">
                  <el-option
                    v-for="item in chamerchandiseForm1"
                    :key="item.suppliergoolsId"
                    :label="item.supName"
                    :value="item.supName">
                  </el-option>
                </el-select>
              </el-form-item>
              <el-form-item label="商品小类型：" prop="supgoolssmallType">
                <el-select v-model="chamerchandiseForm.supgoolssmallType" placeholder="请选择">
                  <el-option
                    v-for="item in chamerchandiseForm1"
                    :key="item.suppliergoolsId"
                    :label="item.supgoolssmallType"
                    :value="item.supgoolssmallType">
                  </el-option>
                </el-select>
              </el-form-item>
              <el-form-item>
                <el-button @click="getMerchandiseList7">查询</el-button>
                <el-button type="primary" @click="chaMerchandiseResetForm">重置</el-button>
              </el-form-item>
            </el-form>
          <el-button type="success" @click="addyonghuDialogVisible = true">新增</el-button>
          <el-button
            type="warning"
            @click="selectedqi"
            :disabled="selectedList.length == 0"
          >批量启用/禁用</el-button>
          <el-button type="danger" @click="selected" :disabled="selectedList.length == 0">批量删除</el-button>
      <el-table :data="merchandiseList" border @selection-change="handleSelectionChange">
            <el-table-column type="selection" width="35" align="center"></el-table-column>
            <el-table-column type="index" width="35" fixed align="center"></el-table-column>
            <el-table-column prop="supId" label="供应商编码" width="100px" align="center"></el-table-column>
            <el-table-column prop="supName" label="供应商名称" width="100px" align="center"></el-table-column>
            <el-table-column prop="supgoolsBigType" label="商品大类型" width="100px" align="center"></el-table-column>
            <el-table-column prop="supgoolsId" label="商品编号" align="center"></el-table-column>
            <el-table-column prop="supgoolsLength" label="尺寸/长" align="center"></el-table-column>
            <el-table-column prop="supgoolsWidth" label="尺寸/宽" align="center"></el-table-column>
            <el-table-column prop="supgoolsHeight" label="尺寸/高" align="center"></el-table-column>
            <el-table-column label="状态" width="65px" align="center">
              <template slot-scope="scope">
                <el-switch
                  v-model="scope.row.supgoolsState"
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
                <el-button type="primary" icon="el-icon-edit" size="mini" @click="showMerchandise(scope.row.suppliergoolsId)">修改</el-button>
                <el-button
                  type="danger"
                  icon="el-icon-delete"
                  @click="deletebumen(scope.row.suppliergoolsId)"
                  size="mini"
                >删除</el-button>
              </template>
            </el-table-column>
          </el-table>
    </el-tab-pane>
    <el-tab-pane label="油墨" >
      <el-form :inline="true" class="demo-form-inline" :model="chamerchandiseForm" ref="chamerchandiseRef">
              <el-form-item label="供应商名称：" prop="supName">
                <el-select v-model="chamerchandiseForm.supName" placeholder="请选择">
                  <el-option
                    v-for="item in chamerchandiseForm1"
                    :key="item.suppliergoolsId"
                    :label="item.supName"
                    :value="item.supName">
                  </el-option>
                </el-select>
              </el-form-item>
              <el-form-item label="商品小类型：" prop="supgoolssmallType">
                <el-select v-model="chamerchandiseForm.supgoolssmallType" placeholder="请选择">
                  <el-option
                    v-for="item in chamerchandiseForm1"
                    :key="item.suppliergoolsId"
                    :label="item.supgoolssmallType"
                    :value="item.supgoolssmallType">
                  </el-option>
                </el-select>
              </el-form-item>
              <el-form-item>
                <el-button @click="getMerchandiseList8">查询</el-button>
                <el-button type="primary" @click="chaMerchandiseResetForm">重置</el-button>
              </el-form-item>
            </el-form>
          <el-button type="success" @click="addyonghuDialogVisible = true">新增</el-button>
          <el-button
            type="warning"
            @click="selectedqi"
            :disabled="selectedList.length == 0"
          >批量启用/禁用</el-button>
          <el-button type="danger" @click="selected" :disabled="selectedList.length == 0">批量删除</el-button>
      <el-table :data="merchandiseList" border @selection-change="handleSelectionChange">
            <el-table-column type="selection" width="35" align="center"></el-table-column>
            <el-table-column type="index" width="35" fixed align="center"></el-table-column>
            <el-table-column prop="supId" label="供应商编码" align="center"></el-table-column>
            <el-table-column prop="supName" label="供应商名称" align="center"></el-table-column>
            <el-table-column prop="supgoolsBigType" label="商品大类型" align="center"></el-table-column>
            <el-table-column prop="supgoolsId" label="商品编号" align="center"></el-table-column>
            <el-table-column prop="supgoolCoated" label="淋膜类型" align="center"></el-table-column>
            <el-table-column label="状态" width="65px" align="center">
              <template slot-scope="scope">
                <el-switch
                  v-model="scope.row.supgoolsState"
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
                <el-button type="primary" icon="el-icon-edit" size="mini" @click="showMerchandise(scope.row.suppliergoolsId)">修改</el-button>
                <el-button
                  type="danger"
                  icon="el-icon-delete"
                  @click="deletebumen(scope.row.suppliergoolsId)"
                  size="mini"
                >删除</el-button>
              </template>
            </el-table-column>
          </el-table>
    </el-tab-pane>
    
    <el-tab-pane label="胶带" >
      <el-form :inline="true" class="demo-form-inline" :model="chamerchandiseForm" ref="chamerchandiseRef">
              <el-form-item label="供应商名称：" prop="supName">
                <el-select v-model="chamerchandiseForm.supName" placeholder="请选择">
                  <el-option
                    v-for="item in chamerchandiseForm1"
                    :key="item.suppliergoolsId"
                    :label="item.supName"
                    :value="item.supName">
                  </el-option>
                </el-select>
              </el-form-item>
              <el-form-item label="商品小类型：" prop="supgoolssmallType">
                <el-select v-model="chamerchandiseForm.supgoolssmallType" placeholder="请选择">
                  <el-option
                    v-for="item in chamerchandiseForm1"
                    :key="item.suppliergoolsId"
                    :label="item.supgoolssmallType"
                    :value="item.supgoolssmallType">
                  </el-option>
                </el-select>
              </el-form-item>
              <el-form-item>
                <el-button @click="getMerchandiseList9">查询</el-button>
                <el-button type="primary" @click="chaMerchandiseResetForm">重置</el-button>
              </el-form-item>
            </el-form>
          <el-button type="success" @click="addyonghuDialogVisible = true">新增</el-button>
          <el-button
            type="warning"
            @click="selectedqi"
            :disabled="selectedList.length == 0"
          >批量启用/禁用</el-button>
          <el-button type="danger" @click="selected" :disabled="selectedList.length == 0">批量删除</el-button>
      <el-table :data="merchandiseList" border @selection-change="handleSelectionChange">
            <el-table-column type="selection" width="35" align="center"></el-table-column>
            <el-table-column type="index" width="35" fixed align="center"></el-table-column>
            <el-table-column prop="supId" label="供应商编码"  align="center"></el-table-column>
            <el-table-column prop="supName" label="供应商名称" align="center"></el-table-column>
            <el-table-column prop="supgoolsBigType" label="商品大类型" align="center"></el-table-column>
            <el-table-column prop="supgoolsId" label="商品编号" align="center"></el-table-column>
            <el-table-column prop="supgoolsBradth" label="宽度" align="center"></el-table-column>
            <el-table-column prop="supgoolsColor" label="颜色" align="center"></el-table-column>
            <el-table-column label="状态" width="65px" align="center">
              <template slot-scope="scope">
                <el-switch
                  v-model="scope.row.supgoolsState"
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
                <el-button type="primary" icon="el-icon-edit" size="mini" @click="showMerchandise(scope.row.suppliergoolsId)">修改</el-button>
                <el-button
                  type="danger"
                  icon="el-icon-delete"
                  @click="deletebumen(scope.row.suppliergoolsId)"
                  size="mini"
                >删除</el-button>
              </template>
            </el-table-column>
          </el-table>
    </el-tab-pane>
  </el-tabs>
    </el-card>
    <el-dialog
      title="新增供应商商品"
      :visible.sync="addyonghuDialogVisible"
      width="48%"
      :before-close="handleClose"
      @closed="dialogClosed"
    >
      <el-form :label-position="labelPosition" label-width="120px" :model="addMerchandiseFrom"
        ref="addMerchandiseRef"
        :rules="addMerchandiseRules">
        <el-row>
          <el-col :span="12">
            <el-form-item label="供应商编号：" prop="supId">
              <el-input placeholder="请输入供应商编号" v-model="addMerchandiseFrom.supId"></el-input>
            </el-form-item>
            <el-form-item label="供应商名称：" prop="supName">
              <el-input placeholder="请输入供应商名称" v-model="addMerchandiseFrom.supName"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="12">
            <el-form-item label="商品编号：" prop="supgoolsId">
              <el-input placeholder="请输入商品编号" v-model="addMerchandiseFrom.supgoolsId"></el-input>
            </el-form-item>
            <el-form-item label="商品大类型：" prop="supgoolsBigType">
          <el-select class="tiantou" placeholder="请选择商品大类型" @change="showshoop"  v-model="addMerchandiseFrom.supgoolsBigType">
            <el-option value="纸张" id="show">纸张</el-option>
            <el-option value="纸箱" id="show">纸箱</el-option>
            <el-option value="袋子" id="show">袋子</el-option>
            <el-option value="油墨" id="show">油墨</el-option>
            <el-option value="胶带" id="show">胶带</el-option>
          </el-select>
        </el-form-item>
          </el-col>
        </el-row>
        <div v-show="bigType == '纸张'">
          <el-form-item label="商品小类型：" prop="supgoolssmallType">
            <el-input placeholder="请输入商品小类型" class="xiang" v-model="addMerchandiseFrom.supgoolssmallType"></el-input>
          </el-form-item>
          <el-form-item label="品牌：" prop="supgoolsBrand">
            <el-input placeholder="请输入品牌" class="xiang" v-model="addMerchandiseFrom.supgoolsBrand"></el-input>
          </el-form-item>
          <el-form-item label="克重：" prop="supgoolsWeight">
            <el-input placeholder="请输入克重" class="xiang" v-model="addMerchandiseFrom.supgoolsWeight"></el-input>
          </el-form-item>
          <el-form-item label="门幅：" prop="supgoolsWidths">
            <el-input placeholder="请输入门幅" class="xiang" v-model="addMerchandiseFrom.supgoolsWidths"></el-input>
          </el-form-item>
          <el-form-item label="淋膜类型：" prop="supgoolCoated">
            <el-input placeholder="请输入淋膜类型" class="xiang" v-model="addMerchandiseFrom.supgoolCoated"></el-input>
          </el-form-item>
        </div>
        <div v-show="bigType == '纸箱'">
          <el-form-item label="商品小类型：" prop="supgoolssmallType">
            <el-input placeholder="请输入商品小类型" class="xiang" v-model="addMerchandiseFrom.supgoolssmallType"></el-input>
          </el-form-item>
          <el-form-item label="克重：" prop="supgoolsWeight">
            <el-input placeholder="请输入克重" class="xiang" v-model="addMerchandiseFrom.supgoolsWeight"></el-input>
          </el-form-item>
        </div>
        <div v-show="bigType == '袋子'">
          <!-- <el-form-item label="商品小类型：" prop="">
            <el-input placeholder="请输入商品小类型" class="xiang"></el-input>
          </el-form-item> -->
          <el-form-item label="尺寸/长：" prop="supgoolsLength">
            <el-input placeholder="请输入尺寸/长" class="xiang" v-model="addMerchandiseFrom.supgoolsLength"></el-input>
          </el-form-item>
          <el-form-item label="尺寸/宽：" prop="supgoolsWidth">
            <el-input placeholder="请输入尺寸/宽" class="xiang" v-model="addMerchandiseFrom.supgoolsWidth"></el-input>
          </el-form-item>
          <el-form-item label="尺寸/高：" prop="supgoolsHeight">
            <el-input placeholder="请输入尺寸/高" class="xiang" v-model="addMerchandiseFrom.supgoolsHeight"></el-input>
          </el-form-item>
        </div>
        <div v-show="bigType == '油墨'">
          <el-form-item label="淋膜类型：" prop="supgoolCoated">
            <el-input placeholder="请输入淋膜类型" class="xiang" v-model="addMerchandiseFrom.supgoolCoated"></el-input>
          </el-form-item>
        </div>
        <div v-show="bigType == '胶带'">
          <el-form-item label="宽度：" prop="supgoolsBradth">
            <el-input placeholder="请输入宽度" class="xiang" v-model="addMerchandiseFrom.supgoolsBradth"></el-input>
          </el-form-item>
          <el-form-item label="颜色：" prop="supgoolsColor">
            <el-input placeholder="请输入颜色" class="xiang" v-model="addMerchandiseFrom.supgoolsColor"></el-input>
          </el-form-item>
        </div>
      </el-form>
      <span slot="footer" class="dialog-footer">
        <el-button @click="addyonghuDialogVisible = false">取 消</el-button>
        <el-button type="primary" @click="addMerchandise">确 定</el-button>
      </span>
    </el-dialog>
    <el-dialog
      title="编辑供应商商品"
      :visible.sync="edityonghuDialogVisible"
      width="48%"
      :before-close="handleClose"
    >
      <el-form :label-position="labelPosition" label-width="120px" :model="editMerchandiseFrom"
        ref="addMerchandiseRef"
        :rules="addMerchandiseRules">
        <el-row>
          <el-col :span="12">
            <el-form-item label="供应商编号：" prop="supId">
              <el-input placeholder="请输入供应商编号" v-model="editMerchandiseFrom.supId"></el-input>
            </el-form-item>
            <el-form-item label="供应商名称：" prop="supName">
              <el-input placeholder="请输入供应商名称" v-model="editMerchandiseFrom.supName"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="12">
            <el-form-item label="商品编号：" prop="supgoolsId">
              <el-input placeholder="请输入商品编号" v-model="editMerchandiseFrom.supgoolsId"></el-input>
            </el-form-item>
            <el-form-item label="商品大类型：" prop="supgoolsBigType">
          <el-select class="tiantou" placeholder="请选择商品大类型" @change="showshoop"  v-model="editMerchandiseFrom.supgoolsBigType">
            <el-option value="纸张" id="show">纸张</el-option>
            <el-option value="纸箱" id="show">纸箱</el-option>
            <el-option value="袋子" id="show">袋子</el-option>
            <el-option value="油墨" id="show">油墨</el-option>
            <el-option value="胶带" id="show">胶带</el-option>
          </el-select>
        </el-form-item>
          </el-col>
        </el-row>
        <div v-show="bigType == '纸张'">
          <el-form-item label="商品小类型：" prop="supgoolssmallType">
            <el-input placeholder="请输入商品小类型" class="xiang" v-model="editMerchandiseFrom.supgoolssmallType"></el-input>
          </el-form-item>
          <el-form-item label="品牌：" prop="supgoolsBrand">
            <el-input placeholder="请输入品牌" class="xiang" v-model="editMerchandiseFrom.supgoolsBrand"></el-input>
          </el-form-item>
          <el-form-item label="克重：" prop="supgoolsWeight">
            <el-input placeholder="请输入克重" class="xiang" v-model="editMerchandiseFrom.supgoolsWeight"></el-input>
          </el-form-item>
          <el-form-item label="门幅：" prop="supgoolsWidths">
            <el-input placeholder="请输入门幅" class="xiang" v-model="editMerchandiseFrom.supgoolsWidths"></el-input>
          </el-form-item>
          <el-form-item label="淋膜类型：" prop="supgoolCoated">
            <el-input placeholder="请输入淋膜类型" class="xiang" v-model="editMerchandiseFrom.supgoolCoated"></el-input>
          </el-form-item>
        </div>
        <div v-show="bigType == '纸箱'">
          <el-form-item label="商品小类型：" prop="supgoolssmallType">
            <el-input placeholder="请输入商品小类型" class="xiang" v-model="editMerchandiseFrom.supgoolssmallType"></el-input>
          </el-form-item>
          <el-form-item label="克重：" prop="supgoolsWeight">
            <el-input placeholder="请输入克重" class="xiang" v-model="editMerchandiseFrom.supgoolsWeight"></el-input>
          </el-form-item>
        </div>
        <div v-show="bigType == '袋子'">
          <el-form-item label="尺寸/长：" prop="supgoolsLength">
            <el-input placeholder="请输入尺寸/长" class="xiang" v-model="editMerchandiseFrom.supgoolsLength"></el-input>
          </el-form-item>
          <el-form-item label="尺寸/宽：" prop="supgoolsWidth">
            <el-input placeholder="请输入尺寸/宽" class="xiang" v-model="editMerchandiseFrom.supgoolsWidth"></el-input>
          </el-form-item>
          <el-form-item label="尺寸/高：" prop="supgoolsHeight">
            <el-input placeholder="请输入尺寸/高" class="xiang" v-model="editMerchandiseFrom.supgoolsHeight"></el-input>
          </el-form-item>
        </div>
        <div v-show="bigType == '油墨'">
          <el-form-item label="淋膜类型：" prop="supgoolCoated">
            <el-input placeholder="请输入淋膜类型" class="xiang" v-model="editMerchandiseFrom.supgoolCoated"></el-input>
          </el-form-item>
        </div>
        <div v-show="bigType == '胶带'">
          <el-form-item label="宽度：" prop="supgoolsBradth">
            <el-input placeholder="请输入宽度" class="xiang" v-model="editMerchandiseFrom.supgoolsBradth"></el-input>
          </el-form-item>
          <el-form-item label="颜色：" prop="supgoolsColor">
            <el-input placeholder="请输入颜色" class="xiang" v-model="editMerchandiseFrom.supgoolsColor"></el-input>
          </el-form-item>
        </div>
      </el-form>
      <span slot="footer" class="dialog-footer">
        <el-button @click="edityonghuDialogVisible = false">取 消</el-button>
        <el-button type="primary" @click="editMerchandise">确 定</el-button>
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
export default {
  data() {
    return {
      value: "",
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
      bigType: "",
      selectedList: [],
      chamerchandiseForm1:[],
      chamerchandiseForm:{
        supName:'',
        supgoolssmallType:'',
        lab:'纸张',
      },
      delarr:[],
      merchandiseList:[],
      addMerchandiseFrom:{
        supgoolsId:'',
        supName:'',
        supgoolsBigType:'',
        supgoolssmallType:'',
        supgoolCoated:'',
        supgoolsBrand:'',
        supgoolsWeight:'',
        supgoolsWidths:'',
        supgoolsBradth:'',
        supgoolsLength:'',
        supgoolsWidth:'',
        supgoolsHeight:'',
        supgoolsColor:'',
        supId:'',
      },

      editMerchandiseFrom:{
        supgoolsId:'',
        supName:'',
        supgoolsBigType:'',
        supgoolssmallType:'',
        supgoolCoated:'',
        supgoolsBrand:'',
        supgoolsWeight:'',
        supgoolsWidths:'',
        supgoolsBradth:'',
        supgoolsLength:'',
        supgoolsWidth:'',
        supgoolsHeight:'',
        supgoolsColor:'',
        supId:'',
      },
      addMerchandiseRules: {
          supName:[
          { required: true, message: '请输入用户名', trigger: 'blur' },
          { min: 3, max: 10, message: '长度在 3 到 10 个字符', trigger: 'blur' }
          ],},
    };
  },
  created() {
    this.getMerchandiseList();
    this.getMerchandiseList1();

  },
  methods: {
   async handleClick(tab) {
        this.chamerchandiseForm.lab=tab.label;
        const { data: res } = await this.$http.get("jc/suppliergoods/selectSuppliergoolslist",{params:this.chamerchandiseForm});
        this.merchandiseList = res;
      },
   async getMerchandiseList(){
      this.chamerchandiseForm.lab=this.chamerchandiseForm.lab;
      const { data: res } = await this.$http.get("jc/suppliergoods/selectSuppliergoolslist",{params:this.chamerchandiseForm});
      this.merchandiseList = res;
    },
    async getMerchandiseList5(){
      this.chamerchandiseForm.lab="纸张";
      const { data: res } = await this.$http.get("jc/suppliergoods/selectSuppliergoolslist",{params:this.chamerchandiseForm});
      this.merchandiseList = res;
    },
    async getMerchandiseList6(){
      this.chamerchandiseForm.lab="纸箱";
      const { data: res } = await this.$http.get("jc/suppliergoods/selectSuppliergoolslist",{params:this.chamerchandiseForm});
      this.merchandiseList = res;
    },
    async getMerchandiseList7(){
      this.chamerchandiseForm.lab="袋子";
      const { data: res } = await this.$http.get("jc/suppliergoods/selectSuppliergoolslist",{params:this.chamerchandiseForm});
      this.merchandiseList = res;
    },
    async getMerchandiseList8(){
      this.chamerchandiseForm.lab="油墨";
      const { data: res } = await this.$http.get("jc/suppliergoods/selectSuppliergoolslist",{params:this.chamerchandiseForm});
      this.merchandiseList = res;
    },
    async getMerchandiseList9(){
      this.chamerchandiseForm.lab="胶带";
      const { data: res } = await this.$http.get("jc/suppliergoods/selectSuppliergoolslist",{params:this.chamerchandiseForm});
      this.merchandiseList = res;
    },
    async getMerchandiseList1(){
      const { data: res } = await this.$http.get("jc/suppliergoods/selectSuppliergoolslist");
      // console.log(res);
      this.chamerchandiseForm1 = res;
    },
    async userStateChanged(userInfo) {
      const { data: res } = await this.$http.post("jc/suppliergoods/updatestate",userInfo);
      this.getMerchandiseList();
    },
    addMerchandise(){
      this.$refs.addMerchandiseRef.validate(async valid => {
        if (!valid) return;   
        console.log(this.addMerchandiseFrom);
        const { data: res } = await this.$http.post("jc/suppliergoods/addSupgools",this.addMerchandiseFrom);
        this.$message.success("用户创建成功！");
        this.getMerchandiseList();
        this.addyonghuDialogVisible = false;
        // this.getSupplierList1();
        // this.getChasupTypelist();
      });
    },
    async showMerchandise(suppliergoolsId){
      let param = new URLSearchParams();
      param.append("suppliergoolsId", suppliergoolsId);
      const {data:res} = await this.$http.post('jc/suppliergoods/selectSugoolsByid',param);
      console.log(res);
      this.editMerchandiseFrom=res;
      this.edityonghuDialogVisible=true;
    },
    async editMerchandise(){
       const {data:res} = await this.$http.post('jc/suppliergoods/updateSupgools',this.editMerchandiseFrom);
       this.getMerchandiseList();
       this.edityonghuDialogVisible=false;
      //  this.getSupplierList1();
      //  this.getChasupTypelist();
    },
    dialogClosed(){
        this.$refs.addMerchandiseRef.resetFields();
      },
      chaMerchandiseResetForm(formName){
        this.$refs.chamerchandiseRef.resetFields();
        this.getMerchandiseList();
    },
    selectedqi(){
      this.delarr=[];
      this.delVisibleqi = true;
      for (let i = 0; i < this.selectedList.length; i++) {
        this.delarr.push({suppliergoolsId:this.selectedList[i].suppliergoolsId,supgoolsState:this.selectedList[i].supgoolsState==1?0:1})
      }
      console.log(this.delarr);
    },
    selected(){
      this.delarr=[];
      this.delVisible = true;
      for (let i = 0; i < this.selectedList.length; i++) {
        this.delarr.push(this.selectedList[i].suppliergoolsId)
      }
      console.log(this.delarr);
    },
    async deleteRow(){
         const {data:res} = await this.$http.post('jc/suppliergoods/deletemoresupgools',this.delarr);
         this.delVisible = false;
         this.getMerchandiseList();
      },
      async deleteRowqi(){
         const {data:res} = await this.$http.post('jc/suppliergoods/updatesupgoolsstate',this.delarr);
         this.delVisibleqi = false;
         this.getMerchandiseList();
      },
    handleSelectionChange(val) {
      console.log(val);
      this.selectedList = val;
    },
    showshoop(value) {
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
      this.$confirm("确认关闭？")
        .then(_ => {
          done();
        })
        .catch(_ => {});
    },
    deletebumen(suppliergoolsId) {
      this.$confirm("此操作将永久删除该职务, 是否继续?", "提示", {
        confirmButtonText: "确定",
        cancelButtonText: "取消",
        type: "warning"
      })
        .then(async () => {
        let param = new URLSearchParams();
        param.append("suppliergoolsId", suppliergoolsId);
        const { data: res } = await this.$http.post(
          "jc/suppliergoods/deleteSupgools",
          param
        );
        this.getMerchandiseList();
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
  width: 230px;
}
.xiang {
  width: 400px;
}
.hu {
  width: 133px;
}
.quan {
  height: 570px;
  float: left;
  margin-right: 20px;
}

.togglr-button {
  width: 120px;
  height: 30px;
  background: #eee;
  text-align: center;
  line-height: 30px;
}
.el-pagination {
  margin-top: 30px;
}
.shu {
  .el-button {
    display: block;
    margin: 0px;
    padding: 10px;
    font-size: 16px;
    color: #999;
  }
  .el-button:hover {
    color: #666;
  }
}
.shoop {
  display: none;
}

</style>
