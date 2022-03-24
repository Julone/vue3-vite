<template>
  <div style="padding: 16px;">
    <h1>文件夹</h1>
    <el-card shadow="hover">
      <el-table :data="tableData" size="small" :border="true">
        <el-table-column prop="id" label="ID" width="140" />
        <el-table-column prop="actor0" label="Actor_0" width="300px" />
        <el-table-column prop="actor1" label="Actor_1" width="300px" />
        <el-table-column prop="CollisionCount" label="碰撞个数" width="60px" />
        <el-table-column label="操作">
          <template #default="scope">
            <el-button
              type="text"
              size="small"
              @click.prevent="onSeeLog(scope.row)"
            >
              查看Log
            </el-button>
          </template>
        </el-table-column>
      </el-table>
    </el-card>
  </div>

  <el-dialog
    v-model="dialogVisible"
    title="日志"
    width="60%"
    :before-close="handleClose"
    :draggable="true"
  >
    <el-card v-loading="logLoading">
      <el-descriptions
        :border="true"
        :column="2"
        direction="vertical"
        v-for="(el, index) in logData"
        :key="index"
        title="Log Info"
      >
        <el-descriptions-item label="Id">{{ el['Id'] }}</el-descriptions-item>
        <el-descriptions-item label="Log">{{ el['Log'] }}</el-descriptions-item>
        <el-descriptions-item label="Parsed">
          {{ el['Parsed'] }}
        </el-descriptions-item>
        <el-descriptions-item label="Time">
          {{ el['Time'] }}
        </el-descriptions-item>
      </el-descriptions>
    </el-card>
    <template #footer>
      <span class="dialog-footer">
        <el-button @click="dialogVisible = false">取消</el-button>
        <el-button type="primary" @click="onSeeReport()">
          查看详细
        </el-button>
      </span>
    </template>
  </el-dialog>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { useRoute, useRouter } from 'vue-router'
import { useStore } from 'vuex'

const item = {
  id: 'cate001',
  actor1: 'bottoms-rig(clone).json',
  actor0: 'earrings-rig(clone).json',
  CollisionCount: 5,
}
const item1 = {
  id: 'cate002',
  actor1: 'bottoms-rig(clone).json',
  actor0: 'earrings-rig(clone).json',
  CollisionCount: 81,
}
const item2 = {
  id: 'cate003',
  actor1: 'bottoms-rig(clone).json',
  actor0: 'earrings-rig(clone).json',
  CollisionCount: 0,
}
const palceholder = [
  { id: '--', actor1: '--', actor0: '--', CollisionCount: '--' },
  { id: '--', actor1: '--', actor0: '--', CollisionCount: '--' },
  { id: '--', actor1: '--', actor0: '--', CollisionCount: '--' },
]
const tableData = ref([item, item1, item2, ...palceholder, ...palceholder])
let logLoading = ref(false)
const logData = ref([])
const router = useRouter()
const store = useStore()
const onSeeReport = () => {
  dialogVisible.value = false
  router.push({ path: '/report/view', query: { id: logData.value[0].Id } })
}
const onSeeLog = data => {
  dialogVisible.value = true
  if (data.isLoaded) {
    return (logData.value = data.logData)
  }
  logLoading.value = true
  setTimeout(() => {
    logLoading.value = false
    data.logData = [
      {
        Id: data.id,
        Log: '2022-03-23-11-33-22.IGGQACD',
        Parsed: true,
        Time: '2022-03-23-11-33-22',
      },
    ]
    logData.value = data.logData
    data.isLoaded = true
  }, 500)
}

const handleClose = (done: () => void) => {
  dialogVisible.value = false
}

const dialogVisible = ref(false)
</script>

<style lang="scss" scoped>
.home {
  color: $mainColor;
}
</style>
