<template>
  <div>
    <div class="onload"><a-button type="primary" @click="downLoad()" style="margin-left: 8px"><a-icon type="printer" />导出/打印</a-button></div>
    <div class="table" id="pdfDom">
      <p class="tiptitle" style="margin-top: 0px">人口学资料及其他信息</p>
      <a-table bordered :data-source="data2" :showHeader="false" :columns="columns2" :pagination="false"> </a-table>
      <p class="tiptitle">知情宣教</p>
      <a-table bordered :data-source="data3" :showHeader="false" :columns="columns3" :pagination="false"> </a-table>
      <p class="tiptitle">知情同意书</p>
      <a-table bordered :data-source="data1" :showHeader="false" :columns="columns" :pagination="false">
        <span slot="age" slot-scope="age">
          <a-radio-group v-model="value1">
            <a-radio :style="radioStyle" :value="1">是</a-radio>
            <a-radio :style="radioStyle" :value="2">否</a-radio>
          </a-radio-group>
        </span>
      </a-table>
      <p class="tiptitle">筛选特殊筛查</p>
      <a-table bordered :data-source="data4" :columns="columns4" :pagination="false"> </a-table>
    </div>
  </div>
</template>

<script>
const columns = [
  {
    title: 'Name',
    dataIndex: 'name',
  },
  {
    title: 'Age',
    dataIndex: 'age',
    width: 160,
    scopedSlots: { customRender: 'age' },
  },
]
const data1 = [
  {
    key: 0,
    name: '是否向该受试者详细解释了本次试验的目的、步骤、可能的受益和风险，及研究程序？',
  },
  {
    key: 1,
    name: '是否向该受试者详细解释了知情同意书的其他全部内容？',
  },
  {
    key: 2,
    name: '是否给予该受试者充分的时间考虑是否参加本次试验？',
  },
  {
    key: 2,
    name: '该受试者是否有机会和研究医生单独讨论研究信息和受试者关心的问题？',
  },
  {
    key: 2,
    name: '该受试者是否充分了解试验目的及药物试验的性质、意义、可能的获益，可带来的不便和潜在的风险，理解研究程序？',
  },
  {
    key: 2,
    name: '该受试者是否自愿参加本次试验？',
  },
  {
    key: 2,
    name: '该受试者是否签署了知情同意书？',
  },
  {
    key: 2,
    name: '是否将一份签好字的知情同意书的原件交给了受试者？',
  },
  {
    key: 2,
    name: '研究者签名：管理员',
  },
  {
    key: 2,
    name: '知情签署时间：2020年09月21日 09时54分',
  },
]
const columns2 = [
  {
    title: 'Name',
    dataIndex: 'name',
  },
]
const data2 = [
  {
    key: 0,
    name: '姓名：测试1',
  },
  {
    key: 1,
    name: '出生日期：1980年02月12日',
  },
  {
    key: 2,
    name: '年龄：40',
  },
  {
    key: 2,
    name: '性别：男',
  },
  {
    key: 2,
    name: '记录者：管理员',
  },
  {
    key: 2,
    name: '民族：汉',
  },
]
const columns3 = [
  {
    title: 'Name',
    dataIndex: 'name',
  },
]
const data3 = [
  {
    name: '宣教内容：',
  },
  {
    name: '提问与答疑：无',
  },
  {
    name: '宣教时间：2020-2-18',
  },
  {
    name: '研究者：管理员',
  },
]
const columns4 = [
  {
    title: '序号',
    dataIndex: 'index',
  },
  {
    title: '检测项目',
    dataIndex: 'item',
  },
  {
    title: '检测时间',
    dataIndex: 'time',
  },
  {
    title: '检测结果',
    dataIndex: 'result',
  },
  {
    title: '检测人',
    dataIndex: 'person',
  },
  {
    title: '核对人',
    dataIndex: 'person2',
  },
  {
    title: '异常备注',
    dataIndex: 'error',
  },
]
const data4 = [
  {
    index: 1,
    item: '烟检',
    person: '李四',
    time: '2020-9-21 09:26',
    result: '阴性',
    person2: '张三',
    error: '无',
  },
  {
    index: 2,
    item: '药筛',
    person: '李四',
    time: '2020-9-21 09:36',
    result: '阴性',
    person2: '张三',
    error: '无',
  },
]
export default {
  data() {
    return { columns, data1, value1: 1, columns2, data2, columns3, data3, fileName:'测试数据', columns4, data4 }
  },
  methods: {
    downLoad() {
      this.getPdf('pdfDom', this.fileName)
    },
  },
}
</script>
<style scoped>
.table {
  padding: 30px;
  width: 1000px;
  margin: 0 auto;
  background: #fff;
  color: #000;
}
.onload{
  width: 1000px;
  margin: 30px auto;
  text-align: right;
}
.topitem {
  text-align: center;
  width: 100%;
  border: solid 1px #333;
  padding: 30px;
  font-size: 24px;
}
.person_msg {
  width: 200px;
  line-height: 40px;
  font-size: 17px;
  margin: 20px auto;
}
.toptitle {
  text-align: center;
  font-size: 34px;
  margin-top: 50px;
}
.topfrom {
  text-align: center;
  font-size: 18px;
  line-height: 34px;
  margin-top: 40px;
}
.top {
  padding-bottom: 200px;
}
.tiptitle {
  font-size: 20px;
  margin-top: 100px;
}
</style>
