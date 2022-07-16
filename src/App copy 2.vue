
<template>
    <div>
        <el-dialog v-model="dialogVisible" title="飞行计划" width="70%" destroy-on-close append-to-body :z-index="1000">
            <el-card shadow="never">
                <el-form :model="currentData" label-width="120px">
                    <el-form-item>
                        <el-date-picker v-model="currentData.time" type="datetime" format="YYYY-MM-DD" placeholder="Select date and time" />
                    </el-form-item>
                </el-form>
            </el-card>
        </el-dialog>
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
const toDay = `${y}-${m}-${d}`

const currentData = ref({
    time: toDay + ' 00:00:00'
})
const dialogVisible = ref(false)

setTimeout(() => {
    dialogVisible.value = true
}, 500);

</script>

<style scoped>
</style>