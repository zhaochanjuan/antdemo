<template>
  <page-header-wrapper>
    <a-card :bordered="false">
      <div class="table-page-search-wrapper">
        <a-form layout="inline">
          <a-row :gutter="48">
            <a-col :md="8" :sm="24">
              <a-form-item label="项目名称">
                <a-input placeholder="请输入项目名称" />
              </a-form-item>
            </a-col>
            <a-col :md="8" :sm="24">
              <a-form-item label="账号名">
                <a-input placeholder="请输入账号名" />
              </a-form-item>
            </a-col>
            <a-col :md="8" :sm="24">
              <a-form-item label="科室">
                <a-select placeholder="请选择" default-value="0">
                  <a-select-option value="0">测试科室1</a-select-option>
                  <a-select-option value="1">测试科室2</a-select-option>
                  <a-select-option value="2">测试科室3</a-select-option>
                </a-select>
              </a-form-item>
            </a-col>
            <a-col :md="8" :sm="24">
              <a-form-item label="角色">
                <a-select placeholder="请选择" default-value="0">
                  <a-select-option value="0">测试角色1</a-select-option>
                  <a-select-option value="1">测试角色2</a-select-option>
                  <a-select-option value="2">测试角色3</a-select-option>
                </a-select>
              </a-form-item>
            </a-col>
            <a-col :md="8" :sm="24">
              <a-form-item label="登录时间">
                <a-date-picker style="width: 100%" placeholder="请选择登录时间" />
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
    dataIndex: 'key',
    key: 'key',
    width: 80,
  },
  {
    title: '登录时间',
    dataIndex: 'time',
    key: 'time',
  },
  {
    title: '账号名',
    dataIndex: 'name',
    key: 'name',
    scopedSlots: { customRender: 'name' },
  },
  {
    title: '项目名称',
    dataIndex: 'project',
    key: 'project',
  },
  {
    title: '科室',
    dataIndex: 'major',
    key: 'major',
  },
  {
    title: '角色',
    dataIndex: 'role',
    key: 'role',
  },
]
const data = [
  {
    key: '1',
    name: 'John Brown',
    major: '测试科室1',
    time: '2021-03-24 15:53:00',
    project: '项目1',
    role: '测试角色1',
  },
  {
    key: '2',
    name: 'Jim Green',
    major: '测试科室2',
    time: '2021-03-24 15:53:00',
    project: '项目2',
    role: '测试角色2',
  },
  {
    key: '3',
    name: 'Joe Black',
    major: '测试科室3',
    time: '2021-03-24 15:53:00',
    project: '项目3',
    role: '测试角色3',
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
