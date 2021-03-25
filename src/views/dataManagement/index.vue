<template>
  <page-header-wrapper>
    <a-card :bordered="false">
      <div class="table-page-search-wrapper">
        <a-form layout="inline">
          <a-row :gutter="48">
            <a-col :md="6" :sm="24">
              <a-form-item label="筛选号">
                <a-input placeholder="" />
              </a-form-item>
            </a-col>
            <a-col :md="6" :sm="24">
              <a-form-item label="随即号">
                <a-input placeholder="" />
              </a-form-item>
            </a-col>
            <a-col :md="6" :sm="24">
              <a-form-item label="当前状态">
                <a-select placeholder="请选择">
                  <a-select-option value="0">筛选</a-select-option>
                  <a-select-option value="1">入组</a-select-option>
                  <a-select-option value="2">出组</a-select-option>
                </a-select>
              </a-form-item>
            </a-col>
            <a-col :md="6" :sm="24">
              <span
                class="table-page-search-submitButtons"
                :style="(advanced && { float: 'right', overflow: 'hidden' }) || {}"
              >
                <a-button type="primary" @click="$refs.table.refresh(true)">查询</a-button>
                <a-button style="margin-left: 8px" @click="() => (this.queryParam = {})">重置</a-button>
              </span>
            </a-col>
            <a-col :md="6" :sm="24">
              <a-button type="primary" @click="yl()"><a-icon type="eye" />预览</a-button>
            
            </a-col>
          </a-row>
        </a-form>
      </div>
      <a-table :columns="columns" :data-source="data" :row-selection="rowSelection" style="margin-top:20px">
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
  },
  {
    title: '状态',
    dataIndex: 'status',
    key: 'status',
  },
  {
    title: '筛选号',
    dataIndex: 'searchnum',
    key: 'searchnum',
  },
  {
    title: '随即号',
    dataIndex: 'num1',
    key: 'num1',
  },
  {
    title: '入组序号',
    dataIndex: 'num2',
    key: 'num2',
  },
  {
    title: '给药顺序号',
    dataIndex: 'num3',
    key: 'num3',
  },
  {
    title: '试验分组',
    dataIndex: 'type',
    key: 'type',
    width: 90,
  },
  {
    title: '试验开始日期',
    dataIndex: 'time1',
    key: 'time1',
    width: 120,
  },
  {
    title: '姓名',
    dataIndex: 'name',
    key: 'name',
    scopedSlots: { customRender: 'name' },
    width: 100,
  },

  {
    title: '姓名缩写',
    dataIndex: 'names',
    key: 'address 2',
  },
  {
    title: '年龄',
    dataIndex: 'age',
    key: 'age',
  },
  {
    title: '出生年月日',
    dataIndex: 'time2',
    key: 'time2',
    ellipsis: true,
    width: 120,
  },
  {
    title: '性别',
    dataIndex: 'sex',
    key: 'sex',
  },
  {
    title: '登记日期',
    dataIndex: 'time3',
    key: 'time3',
    width: 120,
  },
]
const data = [
  {
    key: '1',
    index: '1',
    status: '入组',
    searchnum: '001',
    num1: 'k001',
    num2: '1',
    num3: '1',
    type: '试验组',
    time1: '2020-2-21',
    name: '测试账号1',
    names: 'cs',
    age: '40',
    time2: '1980-02-12',
    sex: '男',
    time3: '2020-2-21',
  },
  {
    key: '2',
    index: '2',
    status: '入组',
    searchnum: '002',
    num1: 'k002',
    num2: '2',
    num3: '2',
    type: '试验组',
    time1: '2020-2-21',
    name: '测试账号2',
    names: 'cs',
    age: '23',
    time2: '2002-11-28',
    sex: '男',
    time3: '2020-2-21',
  },
  {
    key: '3',
    index: '3',
    status: '入组',
    searchnum: '003',
    num1: 'k003',
    num2: '3',
    num3: '3',
    type: '试验组',
    time1: '2020-2-21',
    name: '测试账号3',
    names: 'cs',
    age: '23',
    time2: '2002-11-28',
    sex: '男',
    time3: '2020-2-21',
  },
]

export default {
  data() {
    return {
      data,
      columns,
    }
  },
  computed: {
    rowSelection() {
      return {
        onChange: (selectedRowKeys, selectedRows) => {
          console.log(`selectedRowKeys: ${selectedRowKeys}`, 'selectedRows: ', selectedRows)
        },
        getCheckboxProps: (record) => ({
          props: {
            disabled: record.name === 'Disabled User', // Column configuration not to be checked
            name: record.name,
          },
        }),
      }
    },
  },
  methods:{
    yl(){
       this.$router.push({name:'table'})
    }
  }
}
</script>
<style>
</style>
