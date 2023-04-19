<template>
  <div class="app-container">
    <div>
      <!-- 表格主体 -->
      <el-table v-loading="listLoading" :data="list" element-loading-text="Loading..." border fit highlight-current-row>
        <el-table-column align="center" label="Id" width="95">
          <template slot-scope="scope">
            {{ scope.row.id }}
          </template>
        </el-table-column>
        <el-table-column label="标题" width="115">
          <template slot-scope="scope">
            <el-tag> {{ scope.row.title }}</el-tag>
          </template>
        </el-table-column>
        <el-table-column label="详情" align="center">
          <template slot-scope="scope">
            {{ scope.row.description }}
          </template>
        </el-table-column>
        <el-table-column label="申请人" width="115" align="center">
          <template slot-scope="scope">
            {{ scope.row.applyer }}
          </template>
        </el-table-column>
        <el-table-column label="审批人" width="115" align="center">
          <template slot-scope="scope">
            {{ scope.row.submiter == null ? '暂无':scope.row.submiter }}
          </template>
        </el-table-column>

        <el-table-column label="审批状态" width="115" align="center">
          <template slot-scope="scope">
            <el-tag :type="scope.row.status | statusFilter">
              {{ scope.row.status | statusChinese }}
            </el-tag>
          </template>
        </el-table-column>

        <el-table-column align="center" label="申请开始时间" width="220">
          <template slot-scope="scope">
            <i class="el-icon-time" />
            <span>{{ scope.row.beg_timestamp | parseTime('{y}-{m}-{d} {h}:{i}') }}</span>
          </template>
        </el-table-column>
        <el-table-column align="center" label="申请结束时间" width="220">
          <template slot-scope="scope">
            <i class="el-icon-time" />
            <span>{{ scope.row.end_timestamp | parseTime('{y}-{m}-{d} {h}:{i}') }}</span>
          </template>

        </el-table-column>
        <el-table-column align="center" label="Actions" width="120">
          <template slot-scope="scope">
            <router-link :to="'/apply/edit/'+scope.row.id">
              <el-button type="primary" size="small" icon="el-icon-edit">
                编辑
              </el-button>
            </router-link>
          </template>
        </el-table-column>
      </el-table>
    </div>
  </div>
</template>

<script>
// import { getList } from '@/api/apply'
// import { parseTime } from '@/utils'

export default {
  name: 'Index',
  filters: {
    statusFilter(status) {
      const statusMap = {
        'done': 'success',
        'doing': 'info',
        'redo': 'danger'
      }
      return statusMap[status]
    },
    statusChinese(status) {
      const statusMap = {
        'done': '审批通过',
        'doing': '审批中',
        'redo': '审批不通过'
      }
      return statusMap[status]
    }
  },
  data() {
    return {
      list: null,
      listLoading: false,
      tableKey: 0, // 表格的key, 用于重置表格
      showSubmiter: false
    }
  },

  created() {
    // this.getList()
    this.getList()
  },
  methods: {
    getList() {
      this.list = [
        {
          id: 1,
          title: '标题1',
          description: '详情1',
          applyer: '申请人1',
          beg_timestamp: 1550000000,
          end_timestamp: 1550000001,
          submiter: '审批人1',
          status: 'done'
        },
        {
          id: 2,
          title: '标题2',
          description: '详情2',
          applyer: '申请人2',
          beg_timestamp: 1650000000,
          end_timestamp: 1650000001,
          submiter: null,
          status: 'redo'
        },
        {
          id: 3,
          title: '标题3',
          description: '详情3',
          applyer: '申请人3',
          beg_timestamp: 1750000000,
          end_timestamp: 1750000001,
          submiter: null,
          status: 'doing'
        }
      ]
    },
    // 点击搜索按钮时触发
    handleFilter() {

    },
    // 点击添加按钮时触发
    handleCreate() {

    }
  }

}
</script>

<style></style>
