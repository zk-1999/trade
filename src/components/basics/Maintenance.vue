<template>
    <div class="min1500">
       <!-- 面包屑导航区域 -->
      <el-breadcrumb separator-class="el-icon-arrow-right">
        <el-breadcrumb-item :to="{ path: '/welcome' }">首页</el-breadcrumb-item>
        <el-breadcrumb-item>基础资料</el-breadcrumb-item>
        <el-breadcrumb-item>基础数据维护</el-breadcrumb-item>
      </el-breadcrumb>
      <el-card>
            <el-tabs :tab-position="tabPosition" @tab-click="handleClick" >
            <el-tab-pane label="产品名称" >
              <el-form :inline="true" class="demo-form-inline" :model="chaMaintenanceForm" ref="chaMaintenanceRef">
                    <el-form-item label="名称：" prop="basicRetainone">
                      <el-input placeholder="请输入供应商名称" v-model="chaMaintenanceForm.basicRetainone"></el-input>
                    </el-form-item>
                    <el-form-item>
                        <el-button @click="handleClick(ta)">查询</el-button>
                        <el-button type="success" @click="addyonghuDialogVisible = true">新增</el-button>
                    </el-form-item>
                </el-form>
              <el-table border stripe :data="maintenanceList">
                <el-table-column type="index"></el-table-column>
                <el-table-column prop="basicRetainone" label="名称"></el-table-column>
                <el-table-column prop="basicName" label="所属基础数据"></el-table-column>
                <el-table-column prop="supState" label="状态" width="65px">
              <template slot-scope="scope">
                <!-- {{scope.row}} -->
                <el-switch
                  v-model="scope.row.basicState"
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
                <el-button type="primary" icon="el-icon-edit" size="mini" @click="showEditSupplier(scope.row.basicId)">修改</el-button>
                <el-button
                  type="danger"
                  icon="el-icon-delete"
                  @click="deletebumen(scope.row.basicId)"
                  size="mini"
                >删除</el-button>
              </template>
            </el-table-column>
              </el-table>
              <el-pagination
                @size-change="handleSizeChange"
                @current-change="handleCurrentChange"
                :current-page="currentPage4"
                :page-sizes="[100, 200, 300, 400]"
                :page-size="100"
                layout="total, sizes, prev, pager, next, jumper"
                :total="400">
              </el-pagination>
            </el-tab-pane>
            <el-tab-pane label="产品类型">
              <el-form :inline="true" class="demo-form-inline" :model="chaMaintenanceForm" ref="chaMaintenanceRef">
                    <el-form-item label="名称：" prop="basicRetainone">
                      <el-input placeholder="请输入供应商名称" v-model="chaMaintenanceForm.basicRetainone"></el-input>
                    </el-form-item>
                    <el-form-item>
                        <el-button @click="handleClick(ta)">查询</el-button>
                        <el-button type="success" @click="addyonghuDialogVisible = true">新增</el-button>
                    </el-form-item>
                </el-form>
              <el-table border stripe :data="maintenanceList">
                <el-table-column type="index"></el-table-column>
                <el-table-column prop="basicRetainone" label="名称"></el-table-column>
                <el-table-column prop="basicName" label="所属基础数据"></el-table-column>
                <el-table-column prop="supState" label="状态" width="65px">
              <template slot-scope="scope">
                <!-- {{scope.row}} -->
                <el-switch
                  v-model="scope.row.basicState"
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
                <el-button type="primary" icon="el-icon-edit" size="mini" @click="showEditSupplier(scope.row.basicId)">修改</el-button>
                <el-button
                  type="danger"
                  icon="el-icon-delete"
                  @click="deletebumen(scope.row.basicId)"
                  size="mini"
                >删除</el-button>
              </template>
            </el-table-column>
              </el-table>
              <el-pagination
                @size-change="handleSizeChange"
                @current-change="handleCurrentChange"
                :current-page="currentPage4"
                :page-sizes="[100, 200, 300, 400]"
                :page-size="100"
                layout="total, sizes, prev, pager, next, jumper"
                :total="400">
              </el-pagination>
            </el-tab-pane>
            <el-tab-pane label="产品规格">
             <el-form :inline="true" class="demo-form-inline" :model="chaMaintenanceForm" ref="chaMaintenanceRef">
                    <el-form-item label="名称：" prop="basicRetainone">
                      <el-input placeholder="请输入供应商名称" v-model="chaMaintenanceForm.basicRetainone"></el-input>
                    </el-form-item>
                    <el-form-item>
                        <el-button @click="handleClick(ta)">查询</el-button>
                        <el-button type="success" @click="addyonghuDialogVisible = true">新增</el-button>
                    </el-form-item>
                </el-form>
              <el-table border stripe :data="maintenanceList">
                <el-table-column type="index"></el-table-column>
                <el-table-column prop="basicRetainone" label="名称"></el-table-column>
                <el-table-column prop="basicName" label="所属基础数据"></el-table-column>
                <el-table-column prop="supState" label="状态" width="65px">
              <template slot-scope="scope">
                <!-- {{scope.row}} -->
                <el-switch
                  v-model="scope.row.basicState"
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
                <el-button type="primary" icon="el-icon-edit" size="mini" @click="showEditSupplier(scope.row.basicId)">修改</el-button>
                <el-button
                  type="danger"
                  icon="el-icon-delete"
                  @click="deletebumen(scope.row.basicId)"
                  size="mini"
                >删除</el-button>
              </template>
            </el-table-column>
              </el-table>
              <el-pagination
                @size-change="handleSizeChange"
                @current-change="handleCurrentChange"
                :current-page="currentPage4"
                :page-sizes="[100, 200, 300, 400]"
                :page-size="100"
                layout="total, sizes, prev, pager, next, jumper"
                :total="400">
              </el-pagination>
            </el-tab-pane>
            <el-tab-pane label="纸张品牌">
             <el-form :inline="true" class="demo-form-inline" :model="chaMaintenanceForm" ref="chaMaintenanceRef">
                    <el-form-item label="名称：" prop="basicRetainone">
                      <el-input placeholder="请输入供应商名称" v-model="chaMaintenanceForm.basicRetainone"></el-input>
                    </el-form-item>
                    <el-form-item>
                        <el-button @click="handleClick(ta)">查询</el-button>
                        <el-button type="success" @click="addyonghuDialogVisible = true">新增</el-button>
                    </el-form-item>
                </el-form>
              <el-table border stripe :data="maintenanceList">
                <el-table-column type="index"></el-table-column>
                <el-table-column prop="basicRetainone" label="名称"></el-table-column>
                <el-table-column prop="basicName" label="所属基础数据"></el-table-column>
                <el-table-column prop="supState" label="状态" width="65px">
              <template slot-scope="scope">
                <!-- {{scope.row}} -->
                <el-switch
                  v-model="scope.row.basicState"
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
                <el-button type="primary" icon="el-icon-edit" size="mini" @click="showEditSupplier(scope.row.basicId)">修改</el-button>
                <el-button
                  type="danger"
                  icon="el-icon-delete"
                  @click="deletebumen(scope.row.basicId)"
                  size="mini"
                >删除</el-button>
              </template>
            </el-table-column>
              </el-table>
              <el-pagination
                @size-change="handleSizeChange"
                @current-change="handleCurrentChange"
                :current-page="currentPage4"
                :page-sizes="[100, 200, 300, 400]"
                :page-size="100"
                layout="total, sizes, prev, pager, next, jumper"
                :total="400">
              </el-pagination>
            </el-tab-pane>
            <el-tab-pane label="淋膜类型" >
              <el-form :inline="true" class="demo-form-inline" :model="chaMaintenanceForm" ref="chaMaintenanceRef">
                    <el-form-item label="名称：" prop="basicRetainone">
                      <el-input placeholder="请输入供应商名称" v-model="chaMaintenanceForm.basicRetainone"></el-input>
                    </el-form-item>
                    <el-form-item>
                        <el-button @click="handleClick(ta)">查询</el-button>
                        <el-button type="success" @click="addyonghuDialogVisible = true">新增</el-button>
                    </el-form-item>
                </el-form>
              <el-table border stripe :data="maintenanceList">
                <el-table-column type="index"></el-table-column>
                <el-table-column prop="basicRetainone" label="名称"></el-table-column>
                <el-table-column prop="basicName" label="所属基础数据"></el-table-column>
                <el-table-column prop="supState" label="状态" width="65px">
              <template slot-scope="scope">
                <!-- {{scope.row}} -->
                <el-switch
                  v-model="scope.row.basicState"
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
                <el-button type="primary" icon="el-icon-edit" size="mini" @click="showEditSupplier(scope.row.basicId)">修改</el-button>
                <el-button
                  type="danger"
                  icon="el-icon-delete"
                  @click="deletebumen(scope.row.basicId)"
                  size="mini"
                >删除</el-button>
              </template>
            </el-table-column>
              </el-table>
              <el-pagination
                @size-change="handleSizeChange"
                @current-change="handleCurrentChange"
                :current-page="currentPage4"
                :page-sizes="[100, 200, 300, 400]"
                :page-size="100"
                layout="total, sizes, prev, pager, next, jumper"
                :total="400">
              </el-pagination>
            </el-tab-pane>
            <el-tab-pane label="纸张克重">
             <el-form :inline="true" class="demo-form-inline" :model="chaMaintenanceForm" ref="chaMaintenanceRef">
                    <el-form-item label="名称：" prop="basicRetainone">
                      <el-input placeholder="请输入供应商名称" v-model="chaMaintenanceForm.basicRetainone"></el-input>
                    </el-form-item>
                    <el-form-item>
                        <el-button @click="handleClick(ta)">查询</el-button>
                        <el-button type="success" @click="addyonghuDialogVisible = true">新增</el-button>
                    </el-form-item>
                </el-form>
              <el-table border stripe :data="maintenanceList">
                <el-table-column type="index"></el-table-column>
                <el-table-column prop="basicRetainone" label="名称"></el-table-column>
                <el-table-column prop="basicName" label="所属基础数据"></el-table-column>
                <el-table-column prop="supState" label="状态" width="65px">
              <template slot-scope="scope">
                <!-- {{scope.row}} -->
                <el-switch
                  v-model="scope.row.basicState"
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
                <el-button type="primary" icon="el-icon-edit" size="mini" @click="showEditSupplier(scope.row.basicId)">修改</el-button>
                <el-button
                  type="danger"
                  icon="el-icon-delete"
                  @click="deletebumen(scope.row.basicId)"
                  size="mini"
                >删除</el-button>
              </template>
            </el-table-column>
              </el-table>
              <el-pagination
                @size-change="handleSizeChange"
                @current-change="handleCurrentChange"
                :current-page="currentPage4"
                :page-sizes="[100, 200, 300, 400]"
                :page-size="100"
                layout="total, sizes, prev, pager, next, jumper"
                :total="400">
              </el-pagination>
            </el-tab-pane>
            <el-tab-pane label="配盖">
              <el-form :inline="true" class="demo-form-inline" :model="chaMaintenanceForm" ref="chaMaintenanceRef">
                    <el-form-item label="名称：" prop="basicRetainone">
                      <el-input placeholder="请输入供应商名称" v-model="chaMaintenanceForm.basicRetainone"></el-input>
                    </el-form-item>
                    <el-form-item>
                        <el-button @click="handleClick(ta)">查询</el-button>
                        <el-button type="success" @click="addyonghuDialogVisible = true">新增</el-button>
                    </el-form-item>
                </el-form>
              <el-table border stripe :data="maintenanceList">
                <el-table-column type="index"></el-table-column>
                <el-table-column prop="basicRetainone" label="名称"></el-table-column>
                <el-table-column prop="basicName" label="所属基础数据"></el-table-column>
                <el-table-column prop="supState" label="状态" width="65px">
              <template slot-scope="scope">
                <!-- {{scope.row}} -->
                <el-switch
                  v-model="scope.row.basicState"
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
                <el-button type="primary" icon="el-icon-edit" size="mini" @click="showEditSupplier(scope.row.basicId)">修改</el-button>
                <el-button
                  type="danger"
                  icon="el-icon-delete"
                  @click="deletebumen(scope.row.basicId)"
                  size="mini"
                >删除</el-button>
              </template>
            </el-table-column>
              </el-table>
              <el-pagination
                @size-change="handleSizeChange"
                @current-change="handleCurrentChange"
                :current-page="currentPage4"
                :page-sizes="[100, 200, 300, 400]"
                :page-size="100"
                layout="total, sizes, prev, pager, next, jumper"
                :total="400">
              </el-pagination>
            </el-tab-pane>
            <el-tab-pane label="印刷方式">
              <el-form :inline="true" class="demo-form-inline" :model="chaMaintenanceForm" ref="chaMaintenanceRef">
                    <el-form-item label="名称：" prop="basicRetainone">
                      <el-input placeholder="请输入供应商名称" v-model="chaMaintenanceForm.basicRetainone"></el-input>
                    </el-form-item>
                    <el-form-item>
                        <el-button @click="handleClick(ta)">查询</el-button>
                        <el-button type="success" @click="addyonghuDialogVisible = true">新增</el-button>
                    </el-form-item>
                </el-form>
              <el-table border stripe :data="maintenanceList">
                <el-table-column type="index"></el-table-column>
                <el-table-column prop="basicRetainone" label="名称"></el-table-column>
                <el-table-column prop="basicName" label="所属基础数据"></el-table-column>
                <el-table-column prop="supState" label="状态" width="65px">
              <template slot-scope="scope">
                <!-- {{scope.row}} -->
                <el-switch
                  v-model="scope.row.basicState"
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
                <el-button type="primary" icon="el-icon-edit" size="mini" @click="showEditSupplier(scope.row.basicId)">修改</el-button>
                <el-button
                  type="danger"
                  icon="el-icon-delete"
                  @click="deletebumen(scope.row.basicId)"
                  size="mini"
                >删除</el-button>
              </template>
            </el-table-column>
              </el-table>
              <el-pagination
                @size-change="handleSizeChange"
                @current-change="handleCurrentChange"
                :current-page="currentPage4"
                :page-sizes="[100, 200, 300, 400]"
                :page-size="100"
                layout="total, sizes, prev, pager, next, jumper"
                :total="400">
              </el-pagination>
            </el-tab-pane>
            <el-tab-pane label="库存单位">
              <el-form :inline="true" class="demo-form-inline" :model="chaMaintenanceForm" ref="chaMaintenanceRef">
                    <el-form-item label="名称：" prop="basicRetainone">
                      <el-input placeholder="请输入供应商名称" v-model="chaMaintenanceForm.basicRetainone"></el-input>
                    </el-form-item>
                    <el-form-item>
                        <el-button @click="handleClick(ta)">查询</el-button>
                        <el-button type="success" @click="addyonghuDialogVisible = true">新增</el-button>
                    </el-form-item>
                </el-form>
              <el-table border stripe :data="maintenanceList">
                <el-table-column type="index"></el-table-column>
                <el-table-column prop="basicRetainone" label="名称"></el-table-column>
                <el-table-column prop="basicName" label="所属基础数据"></el-table-column>
                <el-table-column prop="supState" label="状态" width="65px">
              <template slot-scope="scope">
                <!-- {{scope.row}} -->
                <el-switch
                  v-model="scope.row.basicState"
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
                <el-button type="primary" icon="el-icon-edit" size="mini" @click="showEditSupplier(scope.row.basicId)">修改</el-button>
                <el-button
                  type="danger"
                  icon="el-icon-delete"
                  @click="deletebumen(scope.row.basicId)"
                  size="mini"
                >删除</el-button>
              </template>
            </el-table-column>
              </el-table>
              <el-pagination
                @size-change="handleSizeChange"
                @current-change="handleCurrentChange"
                :current-page="currentPage4"
                :page-sizes="[100, 200, 300, 400]"
                :page-size="100"
                layout="total, sizes, prev, pager, next, jumper"
                :total="400">
              </el-pagination>
            </el-tab-pane>
            <el-tab-pane label="供应商类型">
              <el-form :inline="true" class="demo-form-inline" :model="chaMaintenanceForm" ref="chaMaintenanceRef">
                    <el-form-item label="名称：" prop="basicRetainone">
                      <el-input placeholder="请输入供应商名称" v-model="chaMaintenanceForm.basicRetainone"></el-input>
                    </el-form-item>
                    <el-form-item>
                        <el-button @click="handleClick(ta)">查询</el-button>
                        <el-button type="success" @click="addyonghuDialogVisible = true">新增</el-button>
                    </el-form-item>
                </el-form>
              <el-table border stripe :data="maintenanceList">
                <el-table-column type="index"></el-table-column>
                <el-table-column prop="basicRetainone" label="名称"></el-table-column>
                <el-table-column prop="basicName" label="所属基础数据"></el-table-column>
                <el-table-column prop="supState" label="状态" width="65px">
              <template slot-scope="scope">
                <!-- {{scope.row}} -->
                <el-switch
                  v-model="scope.row.basicState"
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
                <el-button type="primary" icon="el-icon-edit" size="mini" @click="showEditSupplier(scope.row.basicId)">修改</el-button>
                <el-button
                  type="danger"
                  icon="el-icon-delete"
                  @click="deletebumen(scope.row.basicId)"
                  size="mini"
                >删除</el-button>
              </template>
            </el-table-column>
              </el-table>
              <el-pagination
                @size-change="handleSizeChange"
                @current-change="handleCurrentChange"
                :current-page="currentPage4"
                :page-sizes="[100, 200, 300, 400]"
                :page-size="100"
                layout="total, sizes, prev, pager, next, jumper"
                :total="400">
              </el-pagination>
            </el-tab-pane>
            <el-tab-pane label="包装类型1">
              <el-form :inline="true" class="demo-form-inline" :model="chaMaintenanceForm" ref="chaMaintenanceRef">
                    <el-form-item label="名称：" prop="basicRetainone">
                      <el-input placeholder="请输入供应商名称" v-model="chaMaintenanceForm.basicRetainone"></el-input>
                    </el-form-item>
                    <el-form-item>
                        <el-button @click="handleClick(ta)">查询</el-button>
                        <el-button type="success" @click="addyonghuDialogVisible = true">新增</el-button>
                    </el-form-item>
                </el-form>
              <el-table border stripe :data="maintenanceList">
                <el-table-column type="index"></el-table-column>
                <el-table-column prop="basicRetainone" label="名称"></el-table-column>
                <el-table-column prop="basicName" label="所属基础数据"></el-table-column>
                <el-table-column prop="supState" label="状态" width="65px">
              <template slot-scope="scope">
                <!-- {{scope.row}} -->
                <el-switch
                  v-model="scope.row.basicState"
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
                <el-button type="primary" icon="el-icon-edit" size="mini" @click="showEditSupplier(scope.row.basicId)">修改</el-button>
                <el-button
                  type="danger"
                  icon="el-icon-delete"
                  @click="deletebumen(scope.row.basicId)"
                  size="mini"
                >删除</el-button>
              </template>
            </el-table-column>
              </el-table>
              <el-pagination
                @size-change="handleSizeChange"
                @current-change="handleCurrentChange"
                :current-page="currentPage4"
                :page-sizes="[100, 200, 300, 400]"
                :page-size="100"
                layout="total, sizes, prev, pager, next, jumper"
                :total="400">
              </el-pagination>
            </el-tab-pane>
            <el-tab-pane label="包装类型2">
              <el-form :inline="true" class="demo-form-inline" :model="chaMaintenanceForm" ref="chaMaintenanceRef">
                    <el-form-item label="名称：" prop="basicRetainone">
                      <el-input placeholder="请输入供应商名称" v-model="chaMaintenanceForm.basicRetainone"></el-input>
                    </el-form-item>
                    <el-form-item>
                        <el-button @click="handleClick(ta)">查询</el-button>
                        <el-button type="success" @click="addyonghuDialogVisible = true">新增</el-button>
                    </el-form-item>
                </el-form>
              <el-table border stripe :data="maintenanceList">
                <el-table-column type="index"></el-table-column>
                <el-table-column prop="basicRetainone" label="名称"></el-table-column>
                <el-table-column prop="basicName" label="所属基础数据"></el-table-column>
                <el-table-column prop="supState" label="状态" width="65px">
              <template slot-scope="scope">
                <!-- {{scope.row}} -->
                <el-switch
                  v-model="scope.row.basicState"
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
                <el-button type="primary" icon="el-icon-edit" size="mini" @click="showEditSupplier(scope.row.basicId)">修改</el-button>
                <el-button
                  type="danger"
                  icon="el-icon-delete"
                  @click="deletebumen(scope.row.basicId)"
                  size="mini"
                >删除</el-button>
              </template>
            </el-table-column>
              </el-table>
              <el-pagination
                @size-change="handleSizeChange"
                @current-change="handleCurrentChange"
                :current-page="currentPage4"
                :page-sizes="[100, 200, 300, 400]"
                :page-size="100"
                layout="total, sizes, prev, pager, next, jumper"
                :total="400">
              </el-pagination>
            </el-tab-pane>
            <el-tab-pane label="货币类型">
              <el-form :inline="true" class="demo-form-inline" :model="chaMaintenanceForm" ref="chaMaintenanceRef">
                    <el-form-item label="名称：" prop="basicRetainone">
                      <el-input placeholder="请输入供应商名称" v-model="chaMaintenanceForm.basicRetainone"></el-input>
                    </el-form-item>
                    <el-form-item>
                        <el-button @click="handleClick(ta)">查询</el-button>
                        <el-button type="success" @click="addyonghuDialogVisible = true">新增</el-button>
                    </el-form-item>
                </el-form>
              <el-table border stripe :data="maintenanceList">
                <el-table-column type="index"></el-table-column>
                <el-table-column prop="basicRetainone" label="名称"></el-table-column>
                <el-table-column prop="basicName" label="所属基础数据"></el-table-column>
                <el-table-column prop="supState" label="状态" width="65px">
              <template slot-scope="scope">
                <!-- {{scope.row}} -->
                <el-switch
                  v-model="scope.row.basicState"
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
                <el-button type="primary" icon="el-icon-edit" size="mini" @click="showEditSupplier(scope.row.basicId)">修改</el-button>
                <el-button
                  type="danger"
                  icon="el-icon-delete"
                  @click="deletebumen(scope.row.basicId)"
                  size="mini"
                >删除</el-button>
              </template>
            </el-table-column>
              </el-table>
              <el-pagination
                @size-change="handleSizeChange"
                @current-change="handleCurrentChange"
                :current-page="currentPage4"
                :page-sizes="[100, 200, 300, 400]"
                :page-size="100"
                layout="total, sizes, prev, pager, next, jumper"
                :total="400">
              </el-pagination>
            </el-tab-pane>
            <el-tab-pane label="收入类型">
              <el-form :inline="true" class="demo-form-inline" :model="chaMaintenanceForm" ref="chaMaintenanceRef">
                    <el-form-item label="名称：" prop="basicRetainone">
                      <el-input placeholder="请输入供应商名称" v-model="chaMaintenanceForm.basicRetainone"></el-input>
                    </el-form-item>
                    <el-form-item>
                        <el-button @click="handleClick(ta)">查询</el-button>
                        <el-button type="success" @click="addyonghuDialogVisible = true">新增</el-button>
                    </el-form-item>
                </el-form>
              <el-table border stripe :data="maintenanceList">
                <el-table-column type="index"></el-table-column>
                <el-table-column prop="basicRetainone" label="名称"></el-table-column>
                <el-table-column prop="basicName" label="所属基础数据"></el-table-column>
                <el-table-column prop="supState" label="状态" width="65px">
              <template slot-scope="scope">
                <!-- {{scope.row}} -->
                <el-switch
                  v-model="scope.row.basicState"
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
                <el-button type="primary" icon="el-icon-edit" size="mini" @click="showEditSupplier(scope.row.basicId)">修改</el-button>
                <el-button
                  type="danger"
                  icon="el-icon-delete"
                  @click="deletebumen(scope.row.basicId)"
                  size="mini"
                >删除</el-button>
              </template>
            </el-table-column>
              </el-table>
              <el-pagination
                @size-change="handleSizeChange"
                @current-change="handleCurrentChange"
                :current-page="currentPage4"
                :page-sizes="[100, 200, 300, 400]"
                :page-size="100"
                layout="total, sizes, prev, pager, next, jumper"
                :total="400">
              </el-pagination>
            </el-tab-pane>
            <el-tab-pane label="支出类型">
              <el-form :inline="true" class="demo-form-inline" :model="chaMaintenanceForm" ref="chaMaintenanceRef">
                    <el-form-item label="名称：" prop="basicRetainone">
                      <el-input placeholder="请输入供应商名称" v-model="chaMaintenanceForm.basicRetainone"></el-input>
                    </el-form-item>
                    <el-form-item>
                        <el-button @click="handleClick(ta)">查询</el-button>
                        <el-button type="success" @click="addyonghuDialogVisible = true">新增</el-button>
                    </el-form-item>
                </el-form>
              <el-table border stripe :data="maintenanceList">
                <el-table-column type="index"></el-table-column>
                <el-table-column prop="basicRetainone" label="名称"></el-table-column>
                <el-table-column prop="basicName" label="所属基础数据"></el-table-column>
                <el-table-column prop="supState" label="状态" width="65px">
              <template slot-scope="scope">
                <!-- {{scope.row}} -->
                <el-switch
                  v-model="scope.row.basicState"
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
                <el-button type="primary" icon="el-icon-edit" size="mini" @click="showEditSupplier(scope.row.basicId)">修改</el-button>
                <el-button
                  type="danger"
                  icon="el-icon-delete"
                  @click="deletebumen(scope.row.basicId)"
                  size="mini"
                >删除</el-button>
              </template>
            </el-table-column>
              </el-table>
              <el-pagination
                @size-change="handleSizeChange"
                @current-change="handleCurrentChange"
                :current-page="currentPage4"
                :page-sizes="[100, 200, 300, 400]"
                :page-size="100"
                layout="total, sizes, prev, pager, next, jumper"
                :total="400">
              </el-pagination>
            </el-tab-pane>
            <el-tab-pane label="产品刀模">
              <el-form :inline="true" class="demo-form-inline" :model="chaMaintenanceForm" ref="chaMaintenanceRef">
                    <el-form-item label="名称：" prop="basicRetainone">
                      <el-input placeholder="请输入供应商名称" v-model="chaMaintenanceForm.basicRetainone"></el-input>
                    </el-form-item>
                    <el-form-item>
                        <el-button @click="handleClick(ta)">查询</el-button>
                        <el-button type="success" @click="addyonghuDialogVisible = true">新增</el-button>
                    </el-form-item>
                </el-form>
              <el-table border stripe :data="maintenanceList">
                <el-table-column type="index"></el-table-column>
                <el-table-column prop="basicRetainone" label="名称"></el-table-column>
                <el-table-column prop="basicName" label="所属基础数据"></el-table-column>
                <el-table-column prop="supState" label="状态" width="65px">
              <template slot-scope="scope">
                <!-- {{scope.row}} -->
                <el-switch
                  v-model="scope.row.basicState"
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
                <el-button type="primary" icon="el-icon-edit" size="mini" @click="showEditSupplier(scope.row.basicId)">修改</el-button>
                <el-button
                  type="danger"
                  icon="el-icon-delete"
                  @click="deletebumen(scope.row.basicId)"
                  size="mini"
                >删除</el-button>
              </template>
            </el-table-column>
              </el-table>
              <el-pagination
                @size-change="handleSizeChange"
                @current-change="handleCurrentChange"
                :current-page="currentPage4"
                :page-sizes="[100, 200, 300, 400]"
                :page-size="100"
                layout="total, sizes, prev, pager, next, jumper"
                :total="400">
              </el-pagination>
            </el-tab-pane>
            <el-tab-pane label="仓库类型">
              <el-form :inline="true" class="demo-form-inline" :model="chaMaintenanceForm" ref="chaMaintenanceRef">
                    <el-form-item label="名称：" prop="basicRetainone">
                      <el-input placeholder="请输入供应商名称" v-model="chaMaintenanceForm.basicRetainone"></el-input>
                    </el-form-item>
                    <el-form-item>
                        <el-button @click="handleClick(ta)">查询</el-button>
                        <el-button type="success" @click="addyonghuDialogVisible = true">新增</el-button>
                    </el-form-item>
                </el-form>
              <el-table border stripe :data="maintenanceList">
                <el-table-column type="index"></el-table-column>
                <el-table-column prop="basicRetainone" label="名称"></el-table-column>
                <el-table-column prop="basicName" label="所属基础数据"></el-table-column>
                <el-table-column prop="supState" label="状态" width="65px">
              <template slot-scope="scope">
                <!-- {{scope.row}} -->
                <el-switch
                  v-model="scope.row.basicState"
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
              <el-pagination
                @size-change="handleSizeChange"
                @current-change="handleCurrentChange"
                :current-page="currentPage4"
                :page-sizes="[100, 200, 300, 400]"
                :page-size="100"
                layout="total, sizes, prev, pager, next, jumper"
                :total="400">
              </el-pagination>
            </el-tab-pane>
            
          </el-tabs>
      </el-card>
      <el-dialog
        title="新增基础数据"
        :visible.sync="addyonghuDialogVisible"
        width="30%"
        :before-close="handleClose">
        <el-form :label-position="labelPosition" label-width="120px" :model="addMaintenance"
        ref="addMaintenanceRef"
        :rules="addMaintenanceRules">
            <el-form-item label="名称：" prop="basicRetainone"><el-input placeholder="请输入名称" v-model="addMaintenance.basicRetainone"></el-input></el-form-item>
            <el-form-item label="所属基础数据："><el-input placeholder="请输入所属基础数据" v-model="ta.label"></el-input></el-form-item>
            <!-- <el-form-item label="状态："><el-input placeholder="请输入状态"></el-input></el-form-item> -->
        </el-form>
        <span slot="footer" class="dialog-footer">
          <el-button @click="addyonghuDialogVisible = false">取 消</el-button>
          <el-button type="primary" @click="addMainte">确 定</el-button>
        </span>
      </el-dialog>
      <el-dialog
        title="编辑基础数据"
        :visible.sync="edityonghuDialogVisible"
        width="30%"
        :before-close="handleClose">
        <el-form :label-position="labelPosition" label-width="120px" :model="editMaintenance"
        ref="addMaintenanceRef"
        :rules="addMaintenanceRules">
          <el-form-item label="名称："><el-input placeholder="请输入名称" v-model="editMaintenance.basicRetainone"></el-input></el-form-item>
          <el-form-item label="所属基础数据"><el-input placeholder="请输入所属基础数据" v-model="ta.label"></el-input></el-form-item>
          <!-- <el-form-item label="状态："><el-input placeholder="请输入状态"></el-input></el-form-item> -->
        </el-form>
        <span slot="footer" class="dialog-footer">
          <el-button @click="edityonghuDialogVisible = false">取 消</el-button>
          <el-button type="primary" @click="editMaint">确 定</el-button>
        </span>
      </el-dialog>
    </div>
</template>
<script>
export default {
  data () {
    return {
        tabPosition: 'left',
        labelPosition: 'right',
        addyonghuDialogVisible: false,
        edityonghuDialogVisible:false,
        resetPassdialogVisible:false,
        currentPage1: 5,
        currentPage2: 5,
        currentPage3: 5,
        currentPage4: 4,
        maintenanceList:[],
        chaMaintenanceForm:{
          basicRetainone:'',
        },
        addMaintenanceRules: {
          basicRetainone:[
          { required: true, message: '请输入用户名', trigger: 'blur' },
          { min: 0, max: 10, message: '长度在 3 到 10 个字符', trigger: 'blur' }
          ],},
        ta:{
          label:'产品名称',
          index:0,
        },
        addMaintenance:{
          basicRetainone:'',
        },
        editMaintenance:{
          basicRetainone:'',
        }
    }
  },
  created () {
    this.handleClick(this.ta);
  },
  methods:{
   async userStateChanged(userInfo) {
      const { data: res } = await this.$http.post("/jc/Basic/updatebasicState",userInfo);
    },
   async handleClick(tab){
     
     this.ta.label=tab.label;
     this.ta.index=tab.index;     
     let param = new URLSearchParams();
     param.append("basicValue", tab.index);
     param.append("basicRetainone", this.chaMaintenanceForm.basicRetainone);
    const { data: res } = await this.$http.post("jc/Basic/selectBasic",param);
    for (let index = 0; index < res.length; index++) {
      res[index].basicName=tab.label;
      
    }
    this.maintenanceList=res;
    this.chaMaintenanceResetForm();
    },
    addMainte(){
      this.$refs.addMaintenanceRef.validate(async valid => {
        if (!valid) return;    
        console.log(this.addMaintenance);
        this.addMaintenance.basicValue=this.ta.index;
        const { data: res } = await this.$http.post("jc/Basic/addBasic",this.addMaintenance);
        this.$message.success("用户创建成功！");
        this.addyonghuDialogVisible = false;
        this.handleClick(this.ta);
      });
    },
    async showEditSupplier(basicId){
      let param = new URLSearchParams();
      param.append("basicId", basicId);
      const {data:res} = await this.$http.post('jc/Basic/selectBasicbyid',param);
      console.log(res);
      this.editMaintenance=res;
      this.edityonghuDialogVisible=true;
    },
    async editMaint(){
       const {data:res} = await this.$http.post('jc/Basic/updateBasic',this.editMaintenance);
       this.edityonghuDialogVisible=false;
       this.handleClick(this.ta);
    },
    chaMaintenanceResetForm(formName){
        this.$refs.chaMaintenanceRef.resetFields();
        // this.handleClick(this.ta);
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
    deletebumen(basicId){
      this.$confirm('此操作将永久删除该职务, 是否继续?', '提示', {
          confirmButtonText: '确定',
          cancelButtonText: '取消',
          type: 'warning'
        }).then(async() => {
          let param = new URLSearchParams();
          param.append("basicId", basicId);
          const { data: res } = await this.$http.post(
            "jc/Basic/deleteBasic",
            param
          );
          this.handleClick(this.ta);
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
      width: 225px;
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
    .fenge{
        width: 100%;
        height: 20px;
        background: #eee;
        margin-top: 15px;
    }
  
    .el-pagination{
        
        margin-top: 10px;
    }
</style>