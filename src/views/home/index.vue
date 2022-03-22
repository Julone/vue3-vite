<template>
  <el-card shadow="hover">
    <el-table :data="tableData" :border="true">
      <el-table-column prop="id" label="ID" width="140" />
      <el-table-column prop="name" label="报告名称" width="240" />
      <el-table-column prop="date" label="日期" width="140" />
      <el-table-column prop="desc" label="描述" />
      <el-table-column label="操作">
        查看Log
      </el-table-column>
    </el-table>
  </el-card>
</template>

<script setup>
import { ref } from 'vue'

const item = {
  id: 'as24-23a3-2b34',
  date: '2016-05-02',
  name: '报告',
  desc: 'No. 189, Grove St, Los Angeles',
}
const tableData = ref(Array.from({ length: 20 }).fill(item))
</script>

<style lang="scss" scoped>
.home {
  color: $mainColor;
}
</style>
