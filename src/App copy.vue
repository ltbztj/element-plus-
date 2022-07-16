
<template>
    <div>
        <el-dialog v-model="dialogVisible" :title="title + '飞行计划'" width="70%" destroy-on-close append-to-body :z-index="1000">
            <!-- <el-card v-if="currentBaseData.id" shadow="never">
                <template #header>
                    <div class="clearfix">
                        <span>审批结果</span>
                    </div>
                </template>
                <el-descriptions class="margin-top" :column="1" border>
                    <el-descriptions-item>
                        <template v-slot:label>
                            审批状态
                        </template>
                        <span style="color:#1890ff">{{ zt }}</span>
                    </el-descriptions-item>
                    <el-descriptions-item>
                        <template v-slot:label>
                            审批意见
                        </template>
                        <span style="color:#1890ff">{{ verify_opinion }}</span>
                    </el-descriptions-item>
                </el-descriptions>
            </el-card> -->

            <el-card shadow="never">
                <template #header><span>基本信息</span></template>
                <el-form ref="baseShowForm_ref" :model="currentBaseData" :rules="formRules" label-width="140px" class="demo-ruleForm" :show-message="false">
                    <el-row :gutter="15">
                        <el-col :xl="6" :lg="8" :md="12" :sm="24">
                            <el-form-item label="关联长期计划编号" prop="fss_task_id">
                                <el-input v-model="currentBaseData.fss_task_id" placeholder="请关联长期计划编号" disabled />
                            </el-form-item>
                        </el-col>
                        <!-- <el-col :xl="6" :lg="8" :md="12" :sm="24">
                            <el-button type="primary" plain @click="dialogVisible_LongTermPlan = true">关联长期计划</el-button>
                        </el-col> -->
                    </el-row>
                    <el-row>
                        <el-col :xl="6" :lg="8" :md="12" :sm="24">
                            <el-form-item label="飞行计划编号" prop="fss_plan_id">
                                <el-input v-model="currentBaseData.fss_plan_id" placeholder="请输入长期计划编号" disabled />
                            </el-form-item>
                        </el-col>
                        <el-col :xl="6" :lg="8" :md="12" :sm="24">
                            <el-form-item label="通航用户" prop="c_name">
                                <el-input v-model="currentBaseData.c_name" placeholder="请输入通航用户" />
                            </el-form-item>
                        </el-col>
                        <!-- <el-col :xl="6" :lg="8" :md="12" :sm="24">
                            <el-form-item label="审批状态" prop="verify_status">
                                <el-input v-model="currentBaseData.verify_status" placeholder="请输入审批状态"/>
                            </el-form-item>
                        </el-col> -->
                        <el-col :xl="6" :lg="8" :md="12" :sm="24">
                            <!-- <el-form-item label="任务性质" prop="fly_quality">
                                <el-tree-select v-model="currentBaseData.fly_quality" default-expand-all node-key="name" placeholder="请输入任务性质" multiple :data="webFlyqualityList" :props="treeProp" />
                            </el-form-item> -->
                        </el-col>
                        <el-col :xl="6" :lg="8" :md="12" :sm="24">
                            <el-form-item label="长期计划开始日期" prop="pre_start_datetime">
                                <el-date-picker v-model="currentBaseData.pre_start_datetime" type="datetime" valueFormat="YYYY-MM-DD HH:mm:ss" format='YYYY-MM-DD HH:mm' placeholder="请选择计划开始日期"></el-date-picker>
                            </el-form-item>
                        </el-col>
                        <el-col :xl="6" :lg="8" :md="12" :sm="24">
                            <el-form-item label="长期计划结束日期" prop="pre_end_datetime">
                                <el-date-picker v-model="currentBaseData.pre_end_datetime" type="datetime" value-format="YYYY-MM-DD HH:mm:ss" format='YYYY-MM-DD HH:mm' placeholder="请选择计划结束日期" />
                            </el-form-item>
                        </el-col>
                        <!-- <el-col :xl="6" :lg="8" :md="12" :sm="24">
                            <el-form-item label="起降点" prop="all_landpoint">
                                <el-input v-model="currentBaseData.all_landpoint" placeholder="请输入起降点"/>
                            </el-form-item>
                        </el-col> -->
                        <!-- <el-col :xl="6" :lg="8" :md="12" :sm="24">
                            <el-form-item label="机型" prop="all_aircrafttype">
                                <el-input v-model="currentBaseData.all_aircrafttype" placeholder="请输入机型"/>
                            </el-form-item>
                        </el-col> -->
                        <!-- <el-col :xl="6" :lg="8" :md="12" :sm="24">
                            <el-form-item label="机号" prop="all_tna">
                                <el-input v-model="currentBaseData.all_tna" placeholder="请输入机号"/>
                            </el-form-item>
                        </el-col> -->
                        <el-col :xl="6" :lg="8" :md="12" :sm="24">
                            <el-form-item label="预计飞行架次" prop="pre_fly_count">
                                <el-input-number v-model="currentBaseData.pre_fly_count" placeholder="请输入预计飞行架次" />
                            </el-form-item>
                        </el-col>
                        <el-col :xl="6" :lg="8" :md="12" :sm="24">
                            <el-form-item label="联系人" prop="contact_person">
                                <el-input v-model="currentBaseData.contact_person" placeholder="请输入联系人" />
                            </el-form-item>
                        </el-col>
                        <el-col :xl="6" :lg="8" :md="12" :sm="24">
                            <el-form-item label="联系电话" prop="contact_phone">
                                <el-input v-model="currentBaseData.contact_phone" placeholder="请输入联系电话" />
                            </el-form-item>
                        </el-col>
                        <el-col :xl="6" :lg="8" :md="12" :sm="24">
                            <el-form-item label="飞行员信息" prop="pilot">
                                <el-input v-model="currentBaseData.pilot" placeholder="请输入飞行员信息" />
                            </el-form-item>
                        </el-col>
                        <el-col :xl="6" :lg="8" :md="12" :sm="24">
                            <el-form-item label="机组人员" prop="aircrew">
                                <el-input v-model="currentBaseData.aircrew" placeholder="请输入机组人员" />
                            </el-form-item>
                        </el-col>
                        <el-col :xl="6" :lg="8" :md="12" :sm="24">
                            <el-form-item label="传真" prop="transactor_fax">
                                <el-input v-model="currentBaseData.transactor_fax" placeholder="请输入传真" />
                            </el-form-item>
                        </el-col>
                        <el-col :xl="6" :lg="8" :md="12" :sm="24">
                            <el-form-item label="承办联系人" prop="transactor_person">
                                <el-input v-model="currentBaseData.transactor_person" placeholder="请输入承办联系人" />
                            </el-form-item>
                        </el-col>
                        <el-col :xl="6" :lg="8" :md="12" :sm="24">
                            <el-form-item label="承办人电话" prop="transactor_phone">
                                <el-input v-model="currentBaseData.transactor_phone" placeholder="请输入承办人电话" />
                            </el-form-item>
                        </el-col>
                        <el-col :xl="6" :lg="8" :md="12" :sm="24">
                            <el-form-item label="是否有外籍人员" prop="has_foreigner">
                                <el-select v-model="currentBaseData.has_foreigner" placeholder="请选择是否有外籍人员">
                                    <el-option v-for="(item, index) in dictObj.whether" :key="index" :label="item.name" :value="item.flag" />
                                </el-select>
                            </el-form-item>
                        </el-col>
                        <el-col :xl="6" :lg="8" :md="12" :sm="24">
                            <el-form-item label="飞行规则" prop="fly_rule">
                                <el-select v-model="currentBaseData.fly_rule" placeholder="请选择是否有外籍人员">
                                    <el-option v-for="(item, index) in dictObj.flyRule" :key="index" :label="item.name" :value="item.flag" />
                                </el-select>
                            </el-form-item>
                        </el-col>
                        <el-col :xl="6" :lg="8" :md="12" :sm="24">
                            <el-form-item label="军航批复" prop="mil_avi_reply">
                                <el-input v-model="currentBaseData.mil_avi_reply" placeholder="请输入军航批复" />
                            </el-form-item>
                        </el-col>
                        <el-col :xl="6" :lg="8" :md="12" :sm="24">
                            <el-form-item label="民航批复" prop="civ_avi_reply">
                                <el-input v-model="currentBaseData.civ_avi_reply" placeholder="请输入民航批复" />
                            </el-form-item>
                        </el-col>
                    </el-row>
                    <el-row>
                        <el-col :xxl="24" :xl="24" :lg="24" :sm="24">
                            <el-form-item label="备注" prop="remark">
                                <el-input type="textarea" v-model="currentBaseData.remark" placeholder="请输入备注" />
                            </el-form-item>
                        </el-col>
                    </el-row>
                    <!-- <el-col :xl="6" :lg="8" :md="12" :sm="24">
                        <el-form-item label="长期计划批复号" prop="fss_task_atc_id">
                            <el-input v-model="currentBaseData.fss_task_atc_id" placeholder="请输入长期计划批复号"/>
                        </el-form-item>
                    </el-col> -->
                    <!-- <el-col :xl="6" :lg="8" :md="12" :sm="24">
                        <el-form-item label="审批意见" prop="verify_opinion">
                            <el-input v-model="currentBaseData.verify_opinion" placeholder="请输入审批意见"/>
                        </el-form-item>
                    </el-col> -->
                    <!-- <el-col :xl="6" :lg="8" :md="12" :sm="24">
                        <el-form-item label="长期计划受理单位" prop="accept_unit">
                            <el-input v-model="currentBaseData.accept_unit" placeholder="请输入长期计划受理单位"/>
                        </el-form-item>
                    </el-col> -->
                    <!-- <el-col :xl="6" :lg="8" :md="12" :sm="24">
                        <el-form-item label="长期计划提交时间" prop="submit_datetime">
                            <el-input v-model="currentBaseData.submit_datetime" placeholder="请输入长期计划提交时间"/>
                        </el-form-item>
                    </el-col> -->
                    <!-- <el-col :xl="6" :lg="8" :md="12" :sm="24">
                        <el-form-item label="涉及单位" prop="refer_unit">
                            <el-input v-model="currentBaseData.refer_unit" placeholder="请输入涉及单位"/>
                        </el-form-item>
                    </el-col> -->
                    <!-- <el-col :xl="6" :lg="8" :md="12" :sm="24">
                        <el-form-item label="服务单位" prop="service_unit">
                            <el-input v-model="currentBaseData.service_unit" placeholder="请输入服务单位"/>
                        </el-form-item>
                    </el-col> -->
                </el-form>
            </el-card>

            <!-- <el-card shadow="never">
                <template #header>
                    <div class="boxBtn" style="margin-bottom: 0;">
                        <span>飞行线路/高度</span>
                        <div class="leftBtn">
                            <el-button type="primary" v-if="operType != 'view'" @click="addFlyingRouteHeight()">新增</el-button>
                            <Toolbar :table="airspace_table_ref" />
                        </div>
                    </div>
                </template>
                <KeepAlive>
                    <ETable :data="state.sectorList" ref="airspace_table_ref" border>
                        <el-table-column label='名称' prop='name' min-width='150'></el-table-column>
                        <el-table-column label='类型' prop='type' min-width='150'></el-table-column>
                        <el-table-column label='代码' prop='code' min-width='150'></el-table-column>
                        <el-table-column label='高度类型' prop='height_type' min-width='150'></el-table-column>
                        <el-table-column label='高度下限' prop='min_height' min-width='150'></el-table-column>
                        <el-table-column label='高度上限' prop='max_height' min-width='150'></el-table-column>
                        <el-table-column label='航路宽度' prop='width' min-width='150'></el-table-column>
                        <el-table-column label='圆形半径' prop='radius' min-width='150'></el-table-column>
                        <el-table-column label='备注' prop='remark' min-width='150'></el-table-column>
                        <el-table-column label='操作' min-width='120' fixed="right" v-if="operType !== 'view'">
                            <template #default="scope">
                                <el-button link type="primary" @click="addFlyingRouteHeight(scope.row, scope.$index)">编辑</el-button>
                                <el-button link type="danger" @click="airspace_del(scope.row, scope.$index)">删除</el-button>
                            </template>
                        </el-table-column>
                    </ETable>
                </KeepAlive>
            </el-card>

            <el-card shadow="never">
                <template #header>
                    <div class="boxBtn">
                        <span>起降点</span>
                        <div class="leftBtn">
                            <el-button type="primary" v-if="operType != 'view'" @click="addLandingAirportPointVisible()">新增</el-button>
                            <Toolbar :table="landingAirportPoint_table_ref" />
                        </div>
                    </div>
                </template>
                <KeepAlive>
                    <ETable :data="state.landingAirportPoint_list" ref="landingAirportPoint_table_ref" border>
                        <el-table-column label='起降点类型' prop='type' min-width='150'>
                            <template #defalut="scope">
                                {{ dictObj.LandPointTypeChoices.find(e => e.flag == scope.row.type)['name'] }}
                            </template>
                        </el-table-column>
                        <el-table-column label='起降点名称' prop='name' min-width='150'></el-table-column>
                        <el-table-column label='经纬度' prop='pos' min-width='150'></el-table-column>
                        <el-table-column label='操作' min-width='120' fixed="right" v-if="operType !== 'view'">
                            <template #default="scope">
                                <el-button link type="primary" @click="addLandingAirportPointVisible(scope.row, scope.$index)">编辑</el-button>
                                <el-button link type="danger" @click="landingAirportPoint_del(scope.row, scope.$index)">删除</el-button>
                            </template>
                        </el-table-column>
                    </ETable>
                </KeepAlive>
            </el-card>

            <el-card shadow="never">
                <template #header>
                    <div class="boxBtn">
                        <span>航空器</span>
                        <div class="leftBtn">
                            <el-button type="primary" v-if="operType != 'view'" @click="addAircraftVisible()">新增</el-button>
                            <Toolbar :table="aircraft_table_ref" />
                        </div>
                    </div>
                </template>
                <KeepAlive>
                    <ETable :data="state.aircraft_list" ref="aircraft_table_ref" border>
                        <el-table-column label='机尾号' prop='tna' min-width='150'></el-table-column>
                        <el-table-column label='机型' prop='type' min-width='150'></el-table-column>
                        <el-table-column label='呼号' prop='callsign' min-width='150'></el-table-column>
                        <el-table-column label='24位地址码' prop='address_code' min-width='150'></el-table-column>
                        <el-table-column label='机载设备' prop='device' min-width='150'></el-table-column>
                        <el-table-column label='是否自有' prop='is_owned' min-width='150'></el-table-column>
                        <el-table-column label='北斗卡号' prop='bd_card_no' min-width='150'></el-table-column>
                        <el-table-column label='是否支持ADS-B' prop='has_adsb' min-width='150'></el-table-column>
                        <el-table-column label='操作' min-width='120' fixed="right" v-if="operType !== 'view'">
                            <template #default="scope">
                                <el-button link type="primary" @click="addAircraftVisible(scope.row, scope.$index)">编辑</el-button>
                                <el-button link type="danger" @click="aircraft_del(scope.row, scope.$index)">删除</el-button>
                            </template>
                        </el-table-column>
                    </ETable>
                </KeepAlive>
            </el-card>

            <el-card shadow="never">
                <template #header><span>附件信息</span></template>
                <el-form ref="ruleFormRef" :model="fileListData" class="demo-ruleForm" :show-message="false" :disabled="operType === 'view'">
                    <el-row>
                        <el-col :xl="6" :lg="8" :md="12" :sm="24">
                            <el-form-item label="附件上传" prop="fss_plan_id">
                                <el-upload v-model:file-list="fileListData.fss_atta_list" class="upload-demo" action="https://run.mocky.io/v3/9d059bf9-4660-45f2-925d-ce80ad6c4d15" multiple :on-preview="handlePreview" :on-remove="handleRemove" :before-remove="beforeRemove" :limit="3" :on-exceed="handleExceed">
                                    <el-button type="primary">点击上传附件</el-button>
                                </el-upload>
                            </el-form-item>
                        </el-col>
                    </el-row>
                </el-form>
            </el-card>

            <template #footer>
                <span class="dialog-footer">
                    <el-button @click="dialogVisible = false">取消</el-button>
                    <el-button type="primary" @click="task_save">保存</el-button>
                </span>
            </template> -->
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

const dictObj = {
    whether: [],
    flyRule: [],
}
const formRules = {}
const dialogVisible = ref(false)
const title = ref('')
const timer = ref(0)
const currentBaseData = ref<any>({
    c_name: '1111222',
    fss_task_id: '',
    fss_plan_id: '',
    verify_status: '',
    fly_quality: [],
    pre_start_datetime: '2020-08-08 00:00:00',
    pre_end_datetime: toDay + ' 23:59:00',
    all_landpoint: '',
    all_aircrafttype: '',
    all_tna: '',
    pre_fly_count: 1,
    contact_person: '',
    contact_phone: '',
    pilot: '',
    aircrew: '',
    transactor_fax: '',
    transactor_person: '',
    transactor_phone: '',
    has_foreigner: '',
    fly_rule: '',
    mil_avi_reply: '',
    civ_avi_reply: '',
    remark: '',
    fss_task_atc_id: '',
    verify_opinion: '',
    accept_unit: '',
    submit_datetime: '',
    refer_unit: '',
    service_unit: '',
    id: ''
})

setTimeout(() => {
    dialogVisible.value = true


    currentBaseData.value.pre_start_datetime = new Date()
}, 1500);

</script>

<style scoped>
</style>