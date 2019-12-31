<template>
  <div class="app-container">
    <el-tabs v-model="tabName" type="card" @tab-click="switchCardClick">
      <el-tab-pane label="全部" name="all">
        <div>
          <el-table
                  v-loading="listLoading"
                  :data="list"
                  element-loading-text="Loading"
                  border
                  fit
                  highlight-current-row
          >
            <el-table-column label="名称" width="100" align="center">
              <template slot-scope="scope">
                {{ scope.row.name }}
              </template>
            </el-table-column>
            <el-table-column label="手机" width="110" align="center">
              <template slot-scope="scope">
                <span>{{ scope.row.mobile }}</span>
              </template>
            </el-table-column>
            <el-table-column label="地区" width="110" align="center">
              <template slot-scope="scope">
                <span>{{ scope.row.area }}</span>
              </template>
            </el-table-column>
            <el-table-column label="注册日期" width="135" align="center">
              <template slot-scope="scope">
                {{ scope.row.registerDate }}
              </template>
            </el-table-column>
            <el-table-column label="分配日期" width="135" align="center">
              <template slot-scope="scope">
                {{ scope.row.registerDate }}
              </template>
            </el-table-column>
            <el-table-column label="签约日期" width="135" align="center">
              <template slot-scope="scope">
                {{ scope.row.registerDate }}
              </template>
            </el-table-column>
            <el-table-column label="签约结果" width="100" align="center">
              <template slot-scope="scope">
                {{ scope.row.other }}
              </template>
            </el-table-column>
            <el-table-column label="其他信息" width="100" align="center">
              <template slot-scope="scope">
                {{ scope.row.other }}
              </template>
            </el-table-column>
            <el-table-column label="Actions" align="center" width="300" class-name="small-padding fixed-width">
              <template slot-scope="{row}">
                <el-button type="primary" size="mini" @click="showDistrbutionDialog=true">
                  分配
                </el-button>
                <el-button type="primary" size="mini" @click="showDialog">
                  修改信息
                </el-button>
                <el-dropdown :hide-on-click="false">
                 <span class="el-dropdown-link">
                    下拉菜单<i class="el-icon-arrow-down el-icon--right"></i>
                  </span>
                    <el-dropdown-menu slot="dropdown">
                      <el-dropdown-item>
                        <el-button type="primary" size="mini" @click="$router.push('/customer/viewInfo')">
                          详细信息
                        </el-button>
                      </el-dropdown-item>
                      <el-dropdown-item>
                        <el-button size="mini" type="success" @click="$router.push('/customer/viewPlan')">
                          查看方案
                        </el-button>
                      </el-dropdown-item>
                      <el-dropdown-item>
                        <el-button size="mini" type="success" @click="$router.push('/customer/editPlan')">
                          添加方案
                        </el-button>
                      </el-dropdown-item>
                    </el-dropdown-menu>
                </el-dropdown>
              </template>
            </el-table-column>
          </el-table>
          <el-pagination
                  style="margin-top: 20px;"
                  background
                  layout="prev, pager, next"
                  :total="1000">
          </el-pagination>
        </div>
      </el-tab-pane>
      <el-tab-pane label="待分配" name="waitDistribution">
      </el-tab-pane>
      <el-tab-pane label="已分配" name="distributioned">
      </el-tab-pane>
      <el-tab-pane label="待处理" name="waitHandle">
      </el-tab-pane>
      <el-tab-pane label="已处理" name="handled">
      </el-tab-pane>
    </el-tabs>
    <el-dialog title="编辑基本信息" :visible.sync="dialogFormVisible" width="25%">
      <el-form label-width="50px">
        <el-form-item label="姓名" >
          <el-input  autocomplete="off" style="width: 240px;"></el-input>
        </el-form-item>
        <el-form-item label="手机" >
          <el-input  autocomplete="off" style="width: 240px;"></el-input>
        </el-form-item>
        <el-form-item label="地区" >
          <el-input  autocomplete="off" style="width: 240px;"></el-input>
        </el-form-item>
        <el-form-item label="信息1" >
          <el-input  autocomplete="off" style="width: 240px;"></el-input>
        </el-form-item>
        <el-form-item label="信息2" >
          <el-input  autocomplete="off" style="width: 240px;"></el-input>
        </el-form-item>
        <el-form-item label="生日">
          <el-date-picker  style="width: 240px;"  type="date" placeholder="选择日期">
          </el-date-picker>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="dialogFormVisible = false">取 消</el-button>
        <el-button type="primary" @click="dialogFormVisible = false">变更</el-button>
      </div>
    </el-dialog>
    <el-dialog title="编辑基本信息" :visible.sync="dialogFormVisible" width="25%">
      <el-form label-width="50px">
        <el-form-item label="姓名" >
          <el-input  autocomplete="off" style="width: 240px;"></el-input>
        </el-form-item>
        <el-form-item label="手机" >
          <el-input  autocomplete="off" style="width: 240px;"></el-input>
        </el-form-item>
        <el-form-item label="地区" >
          <el-input  autocomplete="off" style="width: 240px;"></el-input>
        </el-form-item>
        <el-form-item label="信息1" >
          <el-input  autocomplete="off" style="width: 240px;"></el-input>
        </el-form-item>
        <el-form-item label="信息2" >
          <el-input  autocomplete="off" style="width: 240px;"></el-input>
        </el-form-item>
        <el-form-item label="生日">
          <el-date-picker  style="width: 240px;"  type="date" placeholder="选择日期">
          </el-date-picker>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="dialogFormVisible = false">取 消</el-button>
        <el-button type="primary" @click="dialogFormVisible = false">变更</el-button>
      </div>
    </el-dialog>
    <el-dialog title="分配客户" :visible.sync="showDistrbutionDialog" width="25%">
      <el-form label-width="75px">
        <el-form-item label="客户姓名:" >
          <el-tag type="info">wangjia</el-tag>
        </el-form-item>
        <el-form-item label="客户手机:" >
          <el-tag type="info">187712312312</el-tag>
        </el-form-item>
        <el-form-item label="选择顾问:" >
          <el-input  autocomplete="off" style="width: 240px;"   prefix-icon="el-icon-search"></el-input>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="showDistrbutionDialog = false">取 消</el-button>
        <el-button type="primary" @click="showDistrbutionDialog = false">确认分配</el-button>
      </div>
    </el-dialog>
  </div>
</template>

<script>
  import {getList} from '@/api/table'
  import {dateFormat} from '@/utils/index'

  export default {
    data () {
      return {
        tabName: 'all',
        dialogFormVisible: false,
        showDistrbutionDialog:false,
        list: null,
        listLoading: true
      }
    },
    created () {
      this.fetchData()
    },
    methods: {
      fetchData () {
        let tempList = []
        for (let x = 0; x < 10; x++) {
          tempList.push(({
            name: `习大大${x}`,
            mobile: `186111111${x}`,
            area: `北京`,
            other: 'xxx',
            registerDate: dateFormat(new Date()),
            distributeDate: dateFormat(new Date()),
            contractDate: dateFormat(new Date()),
          }))
        }
        this.list = tempList
        this.listLoading = false
      },
      switchCardClick (tab, event) {
        this.tabName = tab.name
      },
      showDialog (event) {
        this.dialogFormVisible = true
      },
      showDistribution(){
        this.showDistrbutionDialog=true
      }
    }
  }
</script>
