
<template>
    <div>
        <el-form :model="currentBaseData" label-width="120px">
            <el-form-item label="日期1" prop="pre_start_datetime">
                <el-date-picker v-model="currentBaseData.time1" type="datetime" format='YYYY-MM-DD HH:mm' placeholder="请选择计划开始日期"></el-date-picker>
            </el-form-item>
            <el-form-item label="日期2" prop="pre_end_datetime">
                <el-date-picker v-model="currentBaseData.time2" type="datetime" value-format="YYYY-MM-DD HH:mm:ss" format='YYYY-MM-DD HH:mm' placeholder="请选择计划结束日期" />
            </el-form-item>
        </el-form>
    </div>
</template>

<script setup lang="ts">
import { ref } from "vue";
let time = new Date()
let y = time.getFullYear()
let m = time.getMonth() + 1
let d = time.getDate()
if (y.length == 1) y = '0' + y
if (d.length == 1) d = '0' + d
const date = `${y}-${m}-${d}`

const currentBaseData = ref({
    time1: date + ' 00:00:00',
    time2: date + ' 00:00:00'
})


</script>

<style scoped>
</style>