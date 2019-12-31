<template>
  <div class="app-container">
    <el-tabs v-model="tabName" type="card" @tab-click="switchCardClick">
      <el-tab-pane label="债券型基金" name="bondFunds">
        <div>
          <el-table
                  v-loading="listLoading"
                  :data="list"
                  element-loading-text="Loading"
                  border
                  fit
                  highlight-current-row
          >
            <el-table-column label="名称" width="200"  align="center">
              <template slot-scope="scope">
                {{ scope.row.name }}
              </template>
            </el-table-column>
            <el-table-column label="代码" width="110" align="center">
              <template slot-scope="scope">
                <span>{{ scope.row.code }}</span>
              </template>
            </el-table-column>
            <el-table-column label="类型" width="110" align="center">
              <template slot-scope="scope">
                <span>{{ scope.row.type }}</span>
              </template>
            </el-table-column>
            <el-table-column label="最新净值" width="110" align="center">
              <template slot-scope="scope">
                {{ scope.row.netWorth }}
              </template>
            </el-table-column>
            <el-table-column label="更新日期" width="150" align="center">
              <template slot-scope="scope">
                {{ scope.row.date }}
              </template>
            </el-table-column>
            <el-table-column label="Actions" align="center" width="300" class-name="small-padding fixed-width">
              <template slot-scope="{row}">
                <el-button type="primary" size="mini" @click="showDialog">
                  修改净值
                </el-button>
                <el-button size="mini" type="success">
                  查看历史走势
                </el-button>
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
      <el-tab-pane label="股票型基金" name="stockFunds">
        <div>
          <el-table
                  v-loading="listLoading"
                  :data="list"
                  element-loading-text="Loading"
                  border
                  fit
                  highlight-current-row
          >
            <el-table-column label="名称" width="200"  align="center">
              <template slot-scope="scope">
                {{ scope.row.name }}
              </template>
            </el-table-column>
            <el-table-column label="代码" width="110" align="center">
              <template slot-scope="scope">
                <span>{{ scope.row.code }}</span>
              </template>
            </el-table-column>
            <el-table-column label="类型" width="110" align="center">
              <template slot-scope="scope">
                <span>{{ scope.row.type }}</span>
              </template>
            </el-table-column>
            <el-table-column label="最新净值" width="110" align="center">
              <template slot-scope="scope">
                {{ scope.row.netWorth }}
              </template>
            </el-table-column>
            <el-table-column label="更新日期" width="150" align="center">
              <template slot-scope="scope">
                {{ scope.row.date }}
              </template>
            </el-table-column>
            <el-table-column label="Actions" align="center" width="300" class-name="small-padding fixed-width">
              <template slot-scope="{row}">
                <el-button type="primary" size="mini" @click="showDialog">
                  修改净值
                </el-button>
                <el-button size="mini" type="success">
                  查看历史走势
                </el-button>
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
    </el-tabs>
    <el-dialog title="修改净值" :visible.sync="dialogFormVisible" width="25%">
      <el-form label-width="80px">
        <el-form-item label="最新净值" >
          <el-input  autocomplete="off" style="width: 240px;"></el-input>
        </el-form-item>
        <el-form-item label="日期">
          <el-date-picker  style="width: 240px;"  type="date" placeholder="选择日期">
          </el-date-picker>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="dialogFormVisible = false">取 消</el-button>
        <el-button type="primary" @click="dialogFormVisible = false">确 定</el-button>
      </div>
    </el-dialog>


  </div>
</template>

<script>
import { getList } from '@/api/table'
import {dateFormat} from '@/utils/index'

export default {
  filters: {
    statusFilter(status) {
      const statusMap = {
        published: 'success',
        draft: 'gray',
        deleted: 'danger'
      }
      return statusMap[status]
    }
  },
  data() {
    return {
      tabName:'stockFunds',
      dialogFormVisible:false,
      list: null,
      listLoading: true
    }
  },
  created() {
    this.fetchData()
  },
  methods: {
    fetchData() {
      let tempList = []
      for (let x = 0; x < 10; x++) {
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
    }
  }
}
</script>
