<template>
  <div>
    <a-row :gutter="24" type="flex" :style="{ marginTop: '24px' }">
      <a-col :xl="12" :lg="24" :md="24" :sm="24" :xs="24">
        <a-card
          class="antd-pro-pages-dashboard-analysis-salesCard"
          :loading="loading"
          :bordered="false"
          title="登录统计"
          :style="{ minHeight: '400px' }"
        >
          <div slot="extra" style="height: inherit">
            <div class="analysis-salesTypeRadio">
              <a-radio-group defaultValue="b">
                <a-radio-button value="a" @click="changeNow1(0)">上一年</a-radio-button>
                <a-radio-button value="b" @click="changeNow1(1)">今年</a-radio-button>
                <a-radio-button value="c" @click="changeNow1(0)">下一年</a-radio-button>
              </a-radio-group>
            </div>
          </div>
          <div class="no" v-if="barDataValue1 == false">暂无数据</div>
          <bar :data="barData1" v-if="barDataValue1" />
        </a-card>
      </a-col>
      <a-col :xl="12" :lg="24" :md="24" :sm="24" :xs="24">
        <a-card
          class="antd-pro-pages-dashboard-analysis-salesCard"
          :loading="loading"
          :bordered="false"
          title="筛选统计"
          :style="{ minHeight: '400px' }"
        >
          <div slot="extra" style="height: inherit">
            <div class="analysis-salesTypeRadio">
              <a-radio-group defaultValue="b">
                <a-radio-button value="a" @click="changeNow2(0)">上一年</a-radio-button>
                <a-radio-button value="b" @click="changeNow2(1)">今年</a-radio-button>
                <a-radio-button value="c" @click="changeNow2(0)">下一年</a-radio-button>
              </a-radio-group>
            </div>
          </div>
          <div class="no" v-if="barDataValue2 == false">暂无数据</div>
          <bar :data="barData2" v-if="barDataValue2" />
        </a-card>
      </a-col>
    </a-row>

    <div class="antd-pro-pages-dashboard-analysis-twoColLayout" :class="!isMobile && 'desktop'">
      <a-row :gutter="24" type="flex" :style="{ marginTop: '24px' }">
        <a-col :xl="12" :lg="24" :md="24" :sm="24" :xs="24">
          <a-card
            class="antd-pro-pages-dashboard-analysis-salesCard"
            :loading="loading"
            :bordered="false"
            title="导出统计"
            :style="{ minHeight: '400px' }"
          >
            <div slot="extra" style="height: inherit">
              <div class="analysis-salesTypeRadio">
                <a-radio-group defaultValue="b">
                  <a-radio-button value="a" @click="changeNow3(0)">上一月</a-radio-button>
                  <a-radio-button value="b" @click="changeNow3(1)">本月</a-radio-button>
                  <a-radio-button value="c" @click="changeNow3(0)">下一月</a-radio-button>
                </a-radio-group>
              </div>
            </div>
            <div class="no" v-if="barDataValue3 == false">暂无数据</div>
            <a-row :gutter="68" class="export_statistics" v-if="barDataValue3">
              <a-col :xs="24" :sm="24" :style="{ marginBottom: ' 24px' }">
                <number-info :total="12321">
                  <span slot="subtitle">
                    <span>本月导出总数</span>
                  </span>
                </number-info>
                <!-- miniChart -->
                <div>
                  <mini-smooth-area
                    :style="{ widt: '100%', height: '45px' }"
                    :dataSource="searchUserData1"
                    :scale="searchUserScale1"
                  />
                </div>
              </a-col>
            </a-row>
            <div class="ant-table-wrapper" v-if="barDataValue3">
              <a-table
                row-key="index"
                size="small"
                :columns="searchTableColumns1"
                :dataSource="searchData1"
                :pagination="{ pageSize: 5 }"
              >
                <span slot="range" slot-scope="text, record">
                  <trend :flag="record.status === 0 ? 'up' : 'down'"> {{ text }}% </trend>
                </span>
              </a-table>
            </div>
          </a-card>
        </a-col>
        <a-col :xl="12" :lg="24" :md="24" :sm="24" :xs="24">
          <a-card
            class="antd-pro-pages-dashboard-analysis-salesCard"
            :loading="loading"
            :bordered="false"
            title="审批导出统计"
            :style="{ minHeight: '400px' }"
          >
            <div slot="extra" style="height: inherit">
              <div class="analysis-salesTypeRadio">
                <a-radio-group defaultValue="b">
                  <a-radio-button value="a" @click="changeNow4(0)">上一月</a-radio-button>
                  <a-radio-button value="b" @click="changeNow4(1)">本月</a-radio-button>
                  <a-radio-button value="c" @click="changeNow4(0)">下一月</a-radio-button>
                </a-radio-group>
              </div>
            </div>
            <div class="no" v-if="barDataValue4 == false">暂无数据</div>
            <div v-if="barDataValue4">
              <v-chart :force-fit="true" :height="405" :data="pieData" :scale="pieScale">
                <v-tooltip :showTitle="false" dataKey="item*percent" />
                <v-axis />
                <!-- position="right" :offsetX="-140" -->
                <v-legend dataKey="item" />
                <v-pie position="percent" color="item" :vStyle="pieStyle" />
                <v-coord type="theta" :radius="0.75" :innerRadius="0.6" />
              </v-chart>
            </div>
          </a-card>
        </a-col>
      </a-row>
    </div>
    <a-row :gutter="24" type="flex" :style="{ marginTop: '24px' }">
      <a-col :xl="12" :lg="24" :md="24" :sm="24" :xs="24">
        <a-card
          class="antd-pro-pages-dashboard-analysis-salesCard"
          :loading="loading"
          :bordered="false"
          title="下载统计"
          :style="{ minHeight: '400px' }"
        >
          <div slot="extra" style="height: inherit">
            <div class="analysis-salesTypeRadio">
              <a-radio-group defaultValue="b">
                <a-radio-button value="a" @click="changeNow5(0)">上一年</a-radio-button>
                <a-radio-button value="b" @click="changeNow5(1)">今年</a-radio-button>
                <a-radio-button value="c" @click="changeNow5(0)">下一年</a-radio-button>
              </a-radio-group>
            </div>
          </div>
          <div class="no" v-if="barDataValue5 == false">暂无数据</div>
          <bar :data="barData1" v-if="barDataValue5" />
        </a-card>
      </a-col>
      <a-col :xl="12" :lg="24" :md="24" :sm="24" :xs="24">
        <a-card
          class="antd-pro-pages-dashboard-analysis-salesCard"
          :loading="loading"
          :bordered="false"
          title="项目创建统计"
          :style="{ minHeight: '400px' }"
        >
          <div slot="extra" style="height: inherit">
            <div class="analysis-salesTypeRadio">
              <a-radio-group defaultValue="b">
                <a-radio-button value="a" @click="changeNow3(0)">上一月</a-radio-button>
                <a-radio-button value="b" @click="changeNow3(1)">本月</a-radio-button>
                <a-radio-button value="c" @click="changeNow3(0)">下一月</a-radio-button>
              </a-radio-group>
            </div>
          </div>
          <div class="no" v-if="barDataValue3 == false">暂无数据</div>
          <a-row :gutter="68" class="export_statistics" v-if="barDataValue3">
            <a-col :xs="24" :sm="24" :style="{ marginBottom: ' 24px' }">
              <number-info :total="5685">
                <span slot="subtitle">
                  <span>本月项目创建总数</span>
                </span>
              </number-info>
              <!-- miniChart -->
              <div>
                <mini-smooth-area
                  :style="{ widt: '100%', height: '45px' }"
                  :dataSource="searchUserData2"
                  :scale="searchUserScale2"
                />
              </div>
            </a-col>
          </a-row>
          <div class="ant-table-wrapper" v-if="barDataValue3">
            <a-table
              row-key="index"
              size="small"
              :columns="searchTableColumns2"
              :dataSource="searchData2"
              :pagination="{ pageSize: 5 }"
            >
              <span slot="range" slot-scope="text, record">
                <trend :flag="record.status === 0 ? 'up' : 'down'"> {{ text }}% </trend>
              </span>
            </a-table>
          </div>
        </a-card>
      </a-col>
    </a-row>
  </div>
</template>

<script>
import moment from 'moment'
import {
  ChartCard,
  MiniArea,
  MiniBar,
  MiniProgress,
  RankList,
  Bar,
  Trend,
  NumberInfo,
  MiniSmoothArea,
} from '@/components'
import { baseMixin } from '@/store/app-mixin'

const barData1 = []
const barData2 = []
const barObj = new Date()
for (let i = 0; i < 12; i += 1) {
  if (i < barObj.getMonth() + 1) {
    barData1.push({
      x: `${i + 1}月`,
      y: Math.floor(Math.random() * 1000) + 200,
    })
    barData2.push({
      x: `${i + 1}月`,
      y: Math.floor(Math.random() * 1000) + 200,
    })
  } else {
    barData1.push({
      x: `${i + 1}月`,
      y: 0,
    })
    barData2.push({
      x: `${i + 1}月`,
      y: 0,
    })
  }
}

const rankList = []
for (let i = 0; i < 7; i++) {
  rankList.push({
    name: '白鹭岛 ' + (i + 1) + ' 号店',
    total: 1234.56 - i * 100,
  })
}

const searchUserData1 = []
console.log(moment())
if (
  barObj.getMonth() + 1 == 1 ||
  barObj.getMonth() + 1 == 3 ||
  barObj.getMonth() + 1 == 5 ||
  barObj.getMonth() + 1 == 7 ||
  barObj.getMonth() + 1 == 8 ||
  barObj.getMonth() + 1 == 10 ||
  barObj.getMonth() + 1 == 12
) {
  for (let i = 1; i <= 31; i++) {
    if (i < barObj.getDate()) {
      searchUserData1.push({
        x: barObj.getFullYear() + '-' + (barObj.getMonth() + 1) + '-' + i,
        y: Math.ceil(Math.random() * 10),
      })
    } else {
      searchUserData1.push({
        x: barObj.getFullYear() + '-' + (barObj.getMonth() + 1) + '-' + i,
        y: 0,
      })
    }
  }
} else if (barObj.getMonth() + 1 == 2) {
  for (let i = 1; i <= 28; i++) {
    if (i < barObj.getDate()) {
      searchUserData1.push({
        x: barObj.getFullYear() + '-' + (barObj.getMonth() + 1) + '-' + i,
        y: Math.ceil(Math.random() * 10),
      })
    } else {
      searchUserData1.push({
        x: barObj.getFullYear() + '-' + (barObj.getMonth() + 1) + '-' + i,
        y: 0,
      })
    }
  }
} else {
  for (let i = 1; i <= 30; i++) {
    if (i < barObj.getDate()) {
      searchUserData1.push({
        x: barObj.getFullYear() + '-' + (barObj.getMonth() + 1) + '-' + i,
        y: Math.ceil(Math.random() * 10),
      })
    } else {
      searchUserData1.push({
        x: barObj.getFullYear() + '-' + (barObj.getMonth() + 1) + '-' + i,
        y: 0,
      })
    }
  }
}

const searchUserScale1 = [
  {
    dataKey: 'x',
    alias: '时间',
  },
  {
    dataKey: 'y',
    alias: '导出数',
    min: 0,
  },
]

const searchUserData2 = []
console.log(moment())
if (
  barObj.getMonth() + 1 == 1 ||
  barObj.getMonth() + 1 == 3 ||
  barObj.getMonth() + 1 == 5 ||
  barObj.getMonth() + 1 == 7 ||
  barObj.getMonth() + 1 == 8 ||
  barObj.getMonth() + 1 == 10 ||
  barObj.getMonth() + 1 == 12
) {
  for (let i = 1; i <= 31; i++) {
    if (i < barObj.getDate()) {
      searchUserData2.push({
        x: barObj.getFullYear() + '-' + (barObj.getMonth() + 1) + '-' + i,
        y: Math.ceil(Math.random() * 10),
      })
    } else {
      searchUserData2.push({
        x: barObj.getFullYear() + '-' + (barObj.getMonth() + 1) + '-' + i,
        y: 0,
      })
    }
  }
} else if (barObj.getMonth() + 1 == 2) {
  for (let i = 1; i <= 28; i++) {
    if (i < barObj.getDate()) {
      searchUserData2.push({
        x: barObj.getFullYear() + '-' + (barObj.getMonth() + 1) + '-' + i,
        y: Math.ceil(Math.random() * 10),
      })
    } else {
      searchUserData2.push({
        x: barObj.getFullYear() + '-' + (barObj.getMonth() + 1) + '-' + i,
        y: 0,
      })
    }
  }
} else {
  for (let i = 1; i <= 30; i++) {
    if (i < barObj.getDate()) {
      searchUserData2.push({
        x: barObj.getFullYear() + '-' + (barObj.getMonth() + 1) + '-' + i,
        y: Math.ceil(Math.random() * 10),
      })
    } else {
      searchUserData2.push({
        x: barObj.getFullYear() + '-' + (barObj.getMonth() + 1) + '-' + i,
        y: 0,
      })
    }
  }
}

const searchUserScale2 = [
  {
    dataKey: 'x',
    alias: '时间',
  },
  {
    dataKey: 'y',
    alias: '导出数',
    min: 0,
  },
]

const searchData1 = []
for (let i = 0; i < 50; i += 1) {
  searchData1.push({
    index: i + 1,
    time: `2021-3-` + barObj.getDate(),
    name: `测试用户-${i + 1}`,
    major: `测试科室-${i + 1}`,
    project: `测试项目-${i + 1}`,
    field: `测试字段-${i + 1}`,
  })
}
const searchData2 = []
for (let i = 0; i < 50; i += 1) {
  searchData2.push({
    index: i + 1,
    project: `测试项目-${i + 1}`,
    time: `2021-3-` + barObj.getDate(),
    topic: `测试课题-${i + 1}`,
    name: `测试用户-${i + 1}`,
    major: `测试科室-${i + 1}`,
    person: `成员-${i + 1}`,
    num: `测试数量555`,
  })
}

const DataSet = require('@antv/data-set')

const sourceData = [
  { item: '已通过', count: 60, color: '#1890ff' },
  { item: '未通过', count: 10, color: '#f00' },
  { item: '未审核', count: 17, color: '#13c28f' },
  { item: '异常', count: 13, color: '#f19b14' },
]

const pieScale = [
  {
    dataKey: 'percent',
    min: 0,
    formatter: '.0%',
  },
]

const dv = new DataSet.View().source(sourceData)
dv.transform({
  type: 'percent',
  field: 'count',
  dimension: 'item',
  as: 'percent',
  color: 'color',
})
const pieData = dv.rows

export default {
  name: 'Analysis',
  mixins: [baseMixin],
  components: {
    ChartCard,
    MiniArea,
    MiniBar,
    MiniProgress,
    RankList,
    Bar,
    Trend,
    NumberInfo,
    MiniSmoothArea,
  },
  data() {
    return {
      loading: true,
      rankList,

      // 搜索用户数
      searchUserData1,
      searchUserData2,
      searchUserScale1,
      searchUserScale2,
      searchData1,
      searchData2,

      barData1,
      barData2,
      barDataValue1: true,
      barDataValue2: true,
      barDataValue3: true,
      barDataValue4: true,
      barDataValue5: true,

      //
      pieScale,
      pieData,
      sourceData,
      pieStyle: {
        stroke: '#fff',
        lineWidth: 1,
      },
    }
  },
  computed: {
    searchTableColumns1() {
      return [
        {
          dataIndex: 'index',
          title: '序号',
          width: 60,
        },
        {
          dataIndex: 'time',
          title: '导出时间',
        },
        {
          dataIndex: 'name',
          title: '账户名',
        },
        {
          dataIndex: 'major',
          title: '科室',
        },
        {
          dataIndex: 'project',
          title: '项目名称',
        },
        {
          dataIndex: 'field',
          title: '导出字段',
        },
      ]
    },
    searchTableColumns2() {
      return [
        {
          dataIndex: 'index',
          title: '序号',
          width: 50,
        },
        {
          dataIndex: 'project',
          title: '项目名称',
        },
        {
          dataIndex: 'time',
          title: '创建时间',
        },
        {
          dataIndex: 'topic',
          title: '课题名称',
        },
        {
          dataIndex: 'name',
          title: '创建人',
        },
        {
          dataIndex: 'major',
          title: '项目所属科室',
        },
        {
          dataIndex: 'person',
          title: '项目成员',
        },
        {
          dataIndex: 'num',
          title: '患者数量',
        },
      ]
    },
  },
  created() {
    setTimeout(() => {
      this.loading = !this.loading
    }, 1000)
  },
  methods: {
    changeNow1(num) {
      if (num == 0) {
        this.barDataValue1 = false
      } else {
        this.barDataValue1 = true
      }
    },
    changeNow2(num) {
      if (num == 0) {
        this.barDataValue2 = false
      } else {
        this.barDataValue2 = true
      }
    },
    changeNow3(num) {
      if (num == 0) {
        this.barDataValue3 = false
      } else {
        this.barDataValue3 = true
      }
    },
    changeNow4(num) {
      if (num == 0) {
        this.barDataValue4 = false
      } else {
        this.barDataValue4 = true
      }
    },
    changeNow5(num) {
      if (num == 0) {
        this.barDataValue5 = false
      } else {
        this.barDataValue5 = true
      }
    },
  },
}
</script>

<style>
.no {
  width: 100%;
  height: auto;
  font-size: 20px;
  color: #999;
  text-align: center;
  margin: 40px 0;
}
.export_statistics .sub-total {
  display: none !important;
}
</style>
<style lang="less" scoped>
.extra-wrapper {
  line-height: 55px;
  padding-right: 24px;

  .extra-item {
    display: inline-block;
    margin-right: 24px;

    a {
      margin-left: 24px;
    }
  }
}

.antd-pro-pages-dashboard-analysis-twoColLayout {
  position: relative;
  display: flex;
  display: block;
  flex-flow: row wrap;
}

.antd-pro-pages-dashboard-analysis-salesCard {
  height: calc(100% - 24px);
  /deep/ .ant-card-head {
    position: relative;
  }
}

.dashboard-analysis-iconGroup {
  i {
    margin-left: 16px;
    color: rgba(0, 0, 0, 0.45);
    cursor: pointer;
    transition: color 0.32s;
    color: black;
  }
}
.analysis-salesTypeRadio {
  position: absolute;
  right: 54px;
  bottom: 12px;
}
</style>
