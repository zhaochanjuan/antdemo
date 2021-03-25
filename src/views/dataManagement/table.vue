<template>
  <div class="table" id="pdfDom">
    <div class="top">
      <p>国家食品药品监督管理总局批件号：NA<br />方案号：XM-001<br />版本号： 版本日期：2021-2-20<br /></p>
      <p class="topitem">方案题目<br />测试项目</p>
      <p class="toptitle" @click="downLoad()">原始病历</p>
      <ul class="person_msg">
        <li>受试者姓名：测试1</li>
        <li>姓 名 缩 写：CS</li>
        <li>筛 选 号：K001</li>
        <li>入 选 号：001</li>
      </ul>
      <p class="topfrom">
        试验开始日期：2020年09月26日<br />试验完成日期：2020年10月26日<br />研究机构：xx大学第一医院I期临床试验研究室<br />申办单位：我是申办方
      </p>
    </div>
    <p class="tiptitle">知情同意书</p>
    <a-table bordered :data-source="data1" :showHeader="false" :columns="columns" :pagination="false">
      <span slot="age" slot-scope="age">
        <a-radio-group v-model="value1">
          <a-radio :style="radioStyle" :value="1">是</a-radio>
          <a-radio :style="radioStyle" :value="2">否</a-radio>
        </a-radio-group>
      </span>
    </a-table>
    <p class="tiptitle">一般状况</p>
    <a-table bordered :data-source="data2" :showHeader="false" :columns="columns2" :pagination="false"> </a-table>
    <p class="tiptitle">人口学资料及其他信息</p>
    <a-table bordered :data-source="data3" :showHeader="false" :columns="columns3" :pagination="false"> </a-table>
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
]
const columns3 = [
  {
    title: 'Name',
    dataIndex: 'name',
  },
  {
    title: 'Age',
    dataIndex: 'age',
  },
]
const data3 = [
  {
    age: '民族：汉',
    name: '种族：亚裔',
  },
]
export default {
  data() {
    return { columns, data1, value1: 1, columns2, data2, columns3, data3, fileName: '数据导出文件' }
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
  width:1000px;
  margin: 0 auto;
  background: #fff;
  color: #000;
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
