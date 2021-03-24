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
              <a-form-item label="创建人">
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
        <a slot="project" slot-scope="text">{{ text }}</a>
        <span slot="num" slot-scope="num">{{ num }}次</span>
        <span slot="key" slot-scope="key">
            <span v-for="(item,index) in key" :key="index">{{item}}&nbsp;&nbsp;</span>
        </span>
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
    width: 80,
  },
  {
    title: '项目名称',
    dataIndex: 'project',
    key: 'address 2',
    ellipsis: true,
    scopedSlots: { customRender: 'project' },
  },
  {
    title: '创建时间',
    dataIndex: 'time',
    key: 'address 1',
    ellipsis: true,
  },
  {
    title: '课题名称',
    dataIndex: 'item',
    key: 'address 2',
    ellipsis: true,
  },
  {
    title: '创建人',
    dataIndex: 'name',
    key: 'name',
    width: 150,
  },
  {
    title: '项目所属科室',
    dataIndex: 'age',
    key: 'age',
  },

  {
    title: '项目成员',
    dataIndex: 'key',
    key: 'address 3',
    ellipsis: true,
    scopedSlots: { customRender: 'key' },
  },
  {
    title: '患者数量',
    dataIndex: 'personnum',
    key: 'address 3',
    ellipsis: true,
  },
  {
    title: '被导出次数',
    dataIndex: 'num',
    key: 'address 3',
    ellipsis: true,
    scopedSlots: { customRender: 'num' },
  },
]
const data = [
  {
    index: '1',
    name: 'John Brown',
    age: '口腔科',
    time: '2018-11-28 22:14:37',
    key: ['张三', '李四'],
    project: '测试项目1',
    item: '课程名称1',
    personnum: 100,
    num: 20,
  },
  {
    index: '2',
    name: 'Jim Green',
    age: '内分泌科',
    time: '2019-11-28 22:14:37',
    key: ['张三', '李四'],
    project: '测试项目2',
    item: '课程名称2',
    personnum: 100,
    num: 20,
  },
  {
    index: '3',
    name: 'Joe Black',
    age: '耳鼻喉科',
    time: '2020-11-28 22:14:37',
    key: ['张三', '李四'],
    project: '测试项目3',
    item: '课程名称3',
    personnum: 100,
    num: 20,
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
