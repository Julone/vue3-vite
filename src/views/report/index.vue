<template>
  <pro-table
    ref="table"
    title="列表"
    :request="getList"
    :columns="columns"
    :search="searchConfig"
    :pagination="paginationConfig"
    @selectionChange="handleSelectionChange"
  >
    <!-- 工具栏 -->
    <template #toolbar>
      <!-- <el-button type="primary" icon="el-icon-delete" @click="batchDelete">
        批量删除
      </el-button>
      <el-button
        type="primary"
        icon="el-icon-plus"
        @click="$router.push('/test/add')"
      >
        添加一条
      </el-button> -->
      <el-button type="primary" icon="el-icon-refresh" @click="refresh">
        刷新
      </el-button>
    </template>
    <template #operate="scope">
      <!-- <el-button
        size="mini"
        type="primary"
        @click="$router.push(`/test/edit/${scope.row.id}`)"
      >
        编辑
      </el-button> -->
      <el-button size="mini" type="danger">删除</el-button>
    </template>
    <template #screen="scope">
      <el-image
        :src="scope.row.screen"
        :preview-src-list="[scope.row.screen]"
        alt=""
        :lazy="true"
      />
    </template>
  </pro-table>
</template>

<script>
import { defineComponent, reactive, ref, toRefs } from 'vue'

export default defineComponent({
  name: 'testList',
  setup() {
    const state = reactive({
      // 表格列配置，大部分属性跟el-table-column配置一样
      columns: [
        { type: 'selection' },
        { label: '序号', type: 'index' },
        {
          label: '截图',
          prop: 'screen',
          sortable: true,
          width: 180,
          tdSlot: 'screen',
        },
        { label: '服饰名称', prop: 'cloth' },
        {
          label: '操作',
          width: 180,
          align: 'center',
          tdSlot: 'operate', // 自定义单元格内容的插槽名称
        },
      ],
      // 搜索配置
      searchConfig: {
        labelWidth: '90px', // 必须带上单位
        inputWidth: '360px', // 必须带上单位
        fields: [
          {
            label: '状态',
            name: 'status',
            type: 'select',
            defaultValue: 1,
            options: [
              {
                name: '已发布',
                value: 1,
              },
              {
                name: '未发布',
                value: 0,
              },
            ],
          },
          {
            label: '时间范围',
            name: 'datetimerange',
            type: 'datetimerange',
            trueNames: ['startTime', 'endTime'],
            style: { width: '360px' },
            defaultValue: ['2020-10-10 9:00:00', '2020-10-11 18:30:00'],
          },
          {
            label: '冲突数量',
            name: 'num',
            type: 'number',
            min: 0,
            max: 10,
          },
        ],
      },
      // 分页配置
      paginationConfig: {
        layout: 'total, prev, pager, next, sizes', // 分页组件显示哪些功能
        pageSize: 5, // 每页条数
        pageSizes: [5, 10, 20, 50],
        style: { textAlign: 'left' },
      },
      selectedItems: [],
      batchDelete() {
        console.log(state.selectedItems)
      },
      // 选择
      handleSelectionChange(arr) {
        state.selectedItems = arr
      },
      // 请求函数
      async getList(params) {
        console.log(params)
        // params是从组件接收的，包含分页和搜索字段。
        const { data } = await new Promise(rs => {
          setTimeout(() => {
            rs({
              code: 200,
              data: {
                list: [
                  {
                    id: 1,
                    screen:
                      'https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fi1.sinaimg.cn%2Fgm%2Fo%2Fi%2F2008-12-12%2FU2620P115T41D158217F757DT20081212173411.jpg&refer=http%3A%2F%2Fi1.sinaimg.cn&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=auto?sec=1650680974&t=271cbb1f538616912a25d29b91d010ec',
                    cloth: '手套1',
                  },
                  {
                    id: 2,
                    screen:
                      'https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fi1.sinaimg.cn%2Fgm%2Fo%2Fi%2F2008-12-12%2FU2620P115T41D158217F757DT20081212173411.jpg&refer=http%3A%2F%2Fi1.sinaimg.cn&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=auto?sec=1650680974&t=271cbb1f538616912a25d29b91d010ec',
                    cloth: '袜子3',
                  },
                  {
                    id: 3,
                    screen:
                      'https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fi1.sinaimg.cn%2Fgm%2Fo%2Fi%2F2008-12-12%2FU2620P115T41D158217F757DT20081212173411.jpg&refer=http%3A%2F%2Fi1.sinaimg.cn&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=auto?sec=1650680974&t=271cbb1f538616912a25d29b91d010ec',
                    cloth: '手套2',
                  },
                  {
                    id: 4,
                    screen:
                      'https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fi1.sinaimg.cn%2Fgm%2Fo%2Fi%2F2008-12-12%2FU2620P115T41D158217F757DT20081212173411.jpg&refer=http%3A%2F%2Fi1.sinaimg.cn&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=auto?sec=1650680974&t=271cbb1f538616912a25d29b91d010ec',
                    cloth: '袜子4',
                  },
                  {
                    id: 5,
                    screen:
                      'https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fi1.sinaimg.cn%2Fgm%2Fo%2Fi%2F2008-12-12%2FU2620P115T41D158217F757DT20081212173411.jpg&refer=http%3A%2F%2Fi1.sinaimg.cn&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=auto?sec=1650680974&t=271cbb1f538616912a25d29b91d010ec',
                    cloth: '手套8',
                  },
                  {
                    id: 6,
                    screen:
                      'https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fi1.sinaimg.cn%2Fgm%2Fo%2Fi%2F2008-12-12%2FU2620P115T41D158217F757DT20081212173411.jpg&refer=http%3A%2F%2Fi1.sinaimg.cn&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=auto?sec=1650680974&t=271cbb1f538616912a25d29b91d010ec',
                    cloth: '袜子0',
                  },
                ],
                total: 100,
              },
            })
          }, 1000)
        })

        // 必须要返回一个对象，包含data数组和total总数
        return {
          data: data.list,
          total: +data.total,
        }
      },
    })
    const table = ref(null)
    const refresh = () => {
      table.value.refresh()
    }

    return { ...toRefs(state), refresh, table }
  },
})
</script>
