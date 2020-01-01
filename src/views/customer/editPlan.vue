<template>
  <div class="app-container">
    <div class="el-tabs--border-card" style="padding:0 30px 30px 30px;">
      <h3><svg-icon icon-class="guide" /> 方案基本信息</h3>
      <el-form ref="form" :inline="true"  label-width="120px" style="margin-top: 30px;" >
        <el-form-item label="方案名称">
          <el-input v-model="form.name"></el-input>
        </el-form-item>
        <el-form-item label="股权、债权">
          <el-col :span="11">
            <el-input v-model="form.name"></el-input>
          </el-col>
          <el-col class="line" :span="1">、</el-col>
          <el-col :span="11">
            <el-input v-model="form.name"></el-input>
          </el-col>
        </el-form-item>
        <el-form-item label="服务开始时间">
            <el-date-picker type="date" placeholder="选择日期" v-model="form.date1" style="width: 100%;"></el-date-picker>
        </el-form-item>
        <el-form-item label="服务结束时间">
            <el-date-picker type="date" placeholder="选择日期" v-model="form.date1" style="width: 100%;"></el-date-picker>
        </el-form-item>
        <el-form-item label="下行波动">
          <el-input v-model="form.name"><template slot="append">%</template></el-input>
        </el-form-item>
        <el-form-item label="极端情况">
          <el-input v-model="form.name"><template slot="append">%</template></el-input>
        </el-form-item>
        <el-form-item label="规划周期">
          <el-input v-model="form.name"><template slot="append">年</template></el-input>
        </el-form-item>
        <el-form-item label="账户市值合计">
          <el-input v-model="form.name"><template slot="append">%</template></el-input>
        </el-form-item>
        <el-form-item label="IRR">
          <el-input v-model="form.name"><template slot="append">%</template></el-input>
        </el-form-item>
      </el-form>
      <div style="margin:10px 0 0 120px;">
        <el-button type="primary" @click="onSubmit">保存方案</el-button>
        <el-button>取消</el-button>
      </div>
    </div>

    <div class="el-tabs--border-card" style="padding:0 30px 30px 30px;margin-top: 20px;">
      <h3 class="clearfix">
        <svg-icon icon-class="guide" /> 产品
        <el-button type="success" size="small" @click="showDialog" icon="el-icon-plus" style="float: right;">添加产品</el-button>
      </h3>
      <div>
        <el-table
          v-loading="listLoading"
          :data="list"
          element-loading-text="Loading"
          border
          fit
          highlight-current-row
        >
          <el-table-column label="产品名称" width="200"  align="center">
            <template slot-scope="scope">
              {{ scope.row.name }}
            </template>
          </el-table-column>
          <el-table-column label="份额" width="110" align="center">
            <template slot-scope="scope">
              <span>{{ scope.row.code }}</span>
            </template>
          </el-table-column>
          <el-table-column label="市值" width="110" align="center">
            <template slot-scope="scope">
              <span>{{ scope.row.type }}</span>
            </template>
          </el-table-column>
          <el-table-column label="盈亏率" width="110" align="center">
            <template slot-scope="scope">
              {{ scope.row.netWorth }}
            </template>
          </el-table-column>
          <el-table-column label="操作" align="center" width="300" class-name="small-padding fixed-width">
            <template slot-scope="{row}">
              <el-button type="primary" size="mini" @click="showDistrbutionDialog=true" >
                查看记录
              </el-button>
            </template>
          </el-table-column>
        </el-table>
      </div>
    </div>
    <el-dialog title="编辑基本信息" :visible.sync="dialogFormVisible" width="25%">
      <el-form label-width="80px">
        <el-form-item label="姓名：" >
          <el-input  autocomplete="off" style="width: 240px;"></el-input>
        </el-form-item>
        <el-form-item label="手机：" >
          <el-input  autocomplete="off" style="width: 240px;"></el-input>
        </el-form-item>
        <el-form-item label="地区：" >
          <el-input  autocomplete="off" style="width: 240px;"></el-input>
        </el-form-item>
        <el-form-item label="信息1：" >
          <el-input  autocomplete="off" style="width: 240px;"></el-input>
        </el-form-item>
        <el-form-item label="信息2：" >
          <el-input  autocomplete="off" style="width: 240px;"></el-input>
        </el-form-item>
        <el-form-item label="生日：">
          <el-date-picker  style="width: 240px;"  type="date" placeholder="选择日期">
          </el-date-picker>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button size="small" @click="dialogFormVisible = false">取 消</el-button>
        <el-button size="small" type="primary" @click="dialogFormVisible = false">变更</el-button>
      </div>
    </el-dialog>
    <el-dialog title="查看记录" :visible.sync="showDistrbutionDialog" width="34%">
      <div>
        <el-table
          v-loading="listLoading"
          :data="list"
          element-loading-text="Loading"
          border
          fit
          highlight-current-row
        >
          <el-table-column label="成本" width="200"  align="center">
            <template slot-scope="scope">
              {{ scope.row.name }}
            </template>
          </el-table-column>
          <el-table-column label="确认份额" width="110" align="center">
            <template slot-scope="scope">
              <span>{{ scope.row.code }}</span>
            </template>
          </el-table-column>
          <el-table-column label="市值" width="110" align="center">
            <template slot-scope="scope">
              <span>{{ scope.row.type }}</span>
            </template>
          </el-table-column>
          <el-table-column label="日期" width="110" align="center">
            <template slot-scope="scope">
              {{ scope.row.netWorth }}
            </template>
          </el-table-column>
        </el-table>
      </div>
      <!--<div slot="footer" class="dialog-footer">-->
        <!--<el-button size="small" @click="dialogFormVisible = false">取 消</el-button>-->
        <!--<el-button size="small" type="primary" @click="dialogFormVisible = false">确 定</el-button>-->
      <!--</div>-->
    </el-dialog>
  </div>
</template>
<script>
  import { getList } from '@/api/table'
  import {dateFormat} from '@/utils/index'
  export default {
    data() {
      return {
        form: {
          name: '',
          region: '',
          date1: '',
          date2: '',
          delivery: false,
          type: [],
          resource: '',
          desc: '',
          tabName: 'all',
          dialogFormVisible: false,
          showDistrbutionDialog:false,
          list: null,
          listLoading: true
        }
      }
    },
    created() {
      this.fetchData()
    },
    methods: {
      onSubmit() {
        console.log('submit!');
      },
      fetchData() {
        let tempList = []
        for (let x = 0; x < 3; x++) {
          tempList.push(({
            name: `汇添富成长焦点混合${x}`,
            code: `519068${x}`,
            netWorth: `1.00${x}`,
            type: x % 2 === 0 ? '债券型' : '股票型',
            date: dateFormat(new Date())
          }))
        }
        this.list = tempList
        this.listLoading = false

        // this.listLoading = true
        // getList().then(response => {
        //   this.list = response.data.items
        //   this.listLoading = false
        // })
      },
      switchCardClick(tab,event){
        this.tabName=tab.name
      },
      showDialog(event){
        this.dialogFormVisible=true
      },
      showDistribution(){
        this.showDistrbutionDialog=true
      }
    }
  }
</script>

<style >
  .line{
    text-align: center;
  }
  .el-form-item{
    width: 48%;
  }
  .el-form--inline .el-form-item__content{
    width:50%!important;
  }
  .el-dialog__header{
    border-bottom: 1px solid  #eee;
  }
  .el-dialog__footer{
    border-top: 1px solid  #eee;
    padding:15px 20px;
  }
</style>

