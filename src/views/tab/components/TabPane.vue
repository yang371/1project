<template>
  <el-table :data="list" border fit highlight-current-row style="width: 100%">
    <el-table-column
      v-loading="loading"
      align="center"
      label="识别编号"
      width="100"
      element-loading-text="请给我点时间！"
    >
      <template slot-scope="scope">
        <span>{{ scope.row.id }}</span>
      </template>
    </el-table-column>

    <el-table-column width="180px" align="center" label="出现频次">
      <template slot-scope="scope">
        <!--        <span>{{ scope.row.timestamp | parseTime('{y}-{m}-{d} {h}:{i}') }}</span>-->
        <span>{{ scope.row.timestamp }}</span>
        <!--        //数据存到timeline.vue中的-->
      </template>
    </el-table-column>

    <el-table-column width="260px" label="出现位置" align="center">
      <template slot-scope="scope">
        <!--        <span>{{ row.location }}</span>-->
        <!--        <el-tag>{{ row.type }}</el-tag>-->
        <span v-for="number in scope.row.location">
          {{ number }}<el-divider direction="vertical" /></span>
        <!--        <span>01：37</span>-->
        <!--        <el-divider direction="vertical" />-->
        <!--        <span>01：38</span>-->
      </template>
    </el-table-column>

    <el-table-column width="300px" align="center" label="画面预览">
      <template slot-scope="scope">
        <el-button-group>
          <el-button v-for="number in scope.row.preview" icon="el-icon-search" size="mini">位置{{ number }}</el-button>
        </el-button-group>
      </template>
    </el-table-column>

    <el-table-column width="180px" label="存储模块" align="center">
      <!--      <template slot-scope="scope">-->
      <!--        <svg-icon v-for="n in +scope.row.importance" :key="n" icon-class="star" />-->
      <!--      </template>-->
      <template>
        <el-button-group>
          <el-button type="primary" icon="el-icon-edit" size="mini">储存</el-button>
          <el-button type="info" icon="el-icon-delete" size="mini">删除</el-button>

        </el-button-group>
      </template>
    </el-table-column>

    <el-table-column align="center" label="画面回放" width="200">
      <template>

        <el-button round icon="el-icon-video-play">画面回放</el-button>
      </template>
    </el-table-column>

    <el-table-column class-name="status-col" label="生成报告" width="180">
      <template>
        <!--        <el-button :type="row.status | statusFilter">-->
        <!--          {{ row.status }}-->
        <!--        </el-button>-->
        <el-button round icon="el-icon-tickets" type="primary" plain>生成报告</el-button>
      </template>
    </el-table-column>
    <el-table-column width="180px" label="管理表格" align="center">
      <!--      <template slot-scope="scope">-->
      <!--        <svg-icon v-for="n in +scope.row.importance" :key="n" icon-class="star" />-->
      <!--      </template>-->
      <template>
        <el-button-group>
            <el-button type="primary" icon="el-icon-edit" size="mini">刷新</el-button>
            <el-button type="danger" icon="el-icon-delete" size="mini" @click="handleDelete(row,$index)">删除</el-button>
          </el-button-group>
      </template>
    </el-table-column>
  </el-table>
</template>

<script>
import { fetchList } from '@/api/article'

export default {
  filters: {
    statusFilter(status) {
      const statusMap = {
        published: 'success',
        draft: 'info',
        deleted: 'danger'
      }
      return statusMap[status]
    }
  },
  props: {
    type: {
      type: String,
      default: 'CN'
    }
  },
  data() {
    return {
      list: null,
      listQuery: {
        page: 1,
        limit: 5,
        type: this.type,
        sort: '+id'
      },
      loading: false
    }
  },
  created() {
    // var usersitelist = this.$route.params.usersitelist;
    // console.log('query',usersitelist)
    // eslint-disable-next-line no-constant-condition,no-self-compare
    var flagg = localStorage.getItem('flag')
    console.log('flag', flagg)
    // eslint-disable-next-line no-constant-condition
    if (flagg === 'ss') {
      this.ss()
      // eslint-disable-next-line no-empty
    } else if (flagg === 'lcd') {
      this.lcd()
    }
  },
  methods: {
    ss() {
      this.loading = true
      this.$emit('create') // for test
      fetchList(this.listQuery).then(response => {
        // this.list = response.data.items
        this.loading = false
        this.list = [{ 'id': 202104271, 'timestamp': 3, 'location': ['03:35', '05:23', '07:15'], 'preview': 3, 'download': '存储 | 删除', 'reon': '画面回放' },
          { 'id': 202104272, 'timestamp': 2, 'location': ['01:25', '04:32'], 'preview': 2, 'download': '存储 | 删除', 'reon': '画面回放' },
          { 'id': 202104273, 'timestamp': 1, 'location': ['03:45'], 'preview': 1, 'download': '存储 | 删除', 'reon': '画面回放' },
          { 'id': 202104274, 'timestamp': 2, 'location': ['05:15', '06:32'], 'preview': 2, 'download': '存储 | 删除', 'reon': '画面回放' },
          { 'id': 202104275, 'timestamp': 2, 'location': ['03:24', '07:32'], 'preview': 2, 'download': '存储 | 删除', 'reon': '画面回放' }]
        // eslint-disable-next-line no-unused-vars
        var preview = this.list[0].preview
        console.log('response', response)
      })
    },
    lcd() {
      this.loading = true
      this.$emit('create') // for test
      fetchList(this.listQuery).then(response => {
        // this.list = response.data.items
        this.loading = false
        this.list = [{ 'id': 202104271, 'timestamp': 2, 'location': ['02:15', '05:29'], 'preview': 2, 'download': '存储 | 删除', 'reon': '画面回放' },
          { 'id': 202104272, 'timestamp': 1, 'location': ['05:55'], 'preview': 1, 'download': '存储 | 删除', 'reon': '画面回放' },
          { 'id': 202104273, 'timestamp': 3, 'location': ['03:45', '03:11'], 'preview': 3, 'download': '存储 | 删除', 'reon': '画面回放' },
          { 'id': 202104274, 'timestamp': 3, 'location': ['05:15', '06:32', '06:55'], 'preview': 3, 'download': '存储 | 删除', 'reon': '画面回放' },
          { 'id': 202104275, 'timestamp': 1, 'location': ['03:24'], 'preview': 1, 'download': '存储 | 删除', 'reon': '画面回放' }]
        // eslint-disable-next-line no-unused-vars
        var preview = this.list[0].preview
        console.log('response', response)
      })
    },
    handleDelete(row, index) {
      this.$notify({
        title: 'Success',
        message: 'Delete Successfully',
        type: 'success',
        duration: 2000
      })
      this.list.splice(index, 1)
    }
  }
}
</script>

