<template>
  <page-header-wrapper>
    <a-card :bordered="false">
      <div class="table-page-search-wrapper">
        <a-form layout="inline">
          <a-row :gutter="48">
            <a-col :md="8" :sm="24">
              <a-form-item label="项目名称">
                <a-input placeholder="" />
              </a-form-item>
            </a-col>
            <a-col :md="8" :sm="24">
              <a-form-item label="账号名">
                <a-input placeholder="" />
              </a-form-item>
            </a-col>
            <a-col :md="8" :sm="24">
              <a-form-item label="科室">
                <a-select placeholder="请选择">
                  <a-select-option value="0">测试科室1</a-select-option>
                  <a-select-option value="1">测试科室2</a-select-option>
                  <a-select-option value="2">测试科室3</a-select-option>
                </a-select>
              </a-form-item>
            </a-col>
            <a-col :md="8" :sm="24">
              <a-form-item label="导出时间">
                <a-date-picker style="width: 100%" placeholder="请输入更新日期" />
              </a-form-item>
            </a-col>
            <template v-if="advanced">
              <a-col :md="8" :sm="24">
                <a-form-item label="申请人员">
                  <a-input placeholder="" />
                </a-form-item>
              </a-col>
              <a-col :md="8" :sm="24">
                <a-form-item label="描述">
                  <a-input-number style="width: 100%" />
                </a-form-item>
              </a-col>
            </template>
            <a-col :md="(!advanced && 8) || 24" :sm="24">
              <span
                class="table-page-search-submitButtons"
                :style="(advanced && { float: 'right', overflow: 'hidden' }) || {}"
              >
                <a-button type="primary" @click="$refs.table.refresh(true)">查询</a-button>
                <a-button style="margin-left: 8px" @click="() => (this.queryParam = {})">重置</a-button>
              </span>
            </a-col>
          </a-row>
        </a-form>
      </div>
      <a-table :columns="columns" :data-source="data">
        <a slot="name" slot-scope="text">{{ text }}</a>
      </a-table>
    </a-card>
  </page-header-wrapper>
</template>

<script>
const columns = [
  {
    title: '序号',
    dataIndex: 'index',
    key: 'address 4',
    width: 100,
  },
  {
    title: '导出时间',
    dataIndex: 'time',
    key: 'address 1',
    ellipsis: true,
    width:250,
  },
  {
    title: '账户名',
    dataIndex: 'name',
    key: 'name',
    scopedSlots: { customRender: 'name' },
    width:200,
  },
  {
    title: '科室',
    dataIndex: 'age',
    key: 'age',
    width: 200,
  },
  {
    title: '项目',
    dataIndex: 'project',
    key: 'address 2',
    ellipsis: true,
  },
  {
    title: '导出字段',
    dataIndex: 'key',
    key: 'address 3',
    ellipsis: true,
  },
]
const data = [
  {
    index: '1',
    name: 'John Brown',
    age: "口腔科",
    time: '2018-11-28 22:14:37',
    key: '测试字段1',
    project: '测试项目1',
  },
  {
    index: '2',
    name: 'Jim Green',
    age: "内分泌科",
    time: '2019-11-28 22:14:37',
    key: '测试字段2',
    project: '测试项目2',
  },
  {
    index: '3',
    name: 'Joe Black',
    age: "耳鼻喉科",
    time: '2020-11-28 22:14:37',
    key: '测试字段3',
    project: '测试项目3',
  },
]

export default {
  data() {
    return {
      data,
      columns,
    }
  },
}
</script>
<style>
</style>
