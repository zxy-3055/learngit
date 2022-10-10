<template>
  <div>
    <el-card class="box-card">
      <div class="clearfix" style="margin-left: -600px;">
        操作员:<el-select v-model="value" placeholder="请选择">
          <el-option v-for="item in options" :key="item.value" :label="item.label" :value="item.value">
          </el-option>
        </el-select>
        客户名称:<el-select v-model="value" placeholder="请选择">
          <el-option v-for="item in options" :key="item.value" :label="item.label" :value="item.value">
          </el-option>
        </el-select>
        物料名称:<el-select v-model="value" placeholder="请选择">
          <el-option v-for="item in options" :key="item.value" :label="item.label" :value="item.value">
          </el-option>
        </el-select>
      </div>
      <div class="block" style="margin-top: 20px; margin-left: -1000px;">
        <span class="demonstration">选择日期：</span>
        <el-date-picker v-model="value2" type="daterange" align="right" unlink-panels range-separator="至"
          start-placeholder="开始日期" end-placeholder="结束日期" :picker-options="pickerOptions">
        </el-date-picker>
      </div>
    </el-card>
    <el-card style="margin-top: 20px; ">
      <div class="table">
        <table border="1" width="100%">
          <thead>
            <tr class="firstHead">
              <th rowspan="2" colspan="1">
                序号
              </th>
              <th rowspan="2" colspan="1">
                客户名称
              </th>
              <th rowspan="2" colspan="1">
                品种
              </th>
              <th rowspan="1" colspan="2">
                <div>
                  当日
                </div>
                <div>
                  销量(吨)
                  金额(元)
                </div>
              </th>
              <th rowspan="2" colspan="1">
                当日回款
              </th>
              <th rowspan="1" colspan="2">
                <div>
                  当月累计
                </div>
                <div>
                  销量(吨)
                  金额(元)
                </div>
              </th>
              <th rowspan="2" colspan="1">
                当月累计汇款
              </th>
              <th rowspan="2" colspan="1">
                当日余额
              </th>
            </tr>

          </thead>
          <tbody v-for="arr in arrList" :key="arr.id">
            <tr v-for="(ac,idx) in arr.category" :key="idx">
              <td :rowspan="arr.category.length+1" v-show="idx == 0">{{arr.id}}</td>
              <td :rowspan="arr.category.length" v-show="idx == 0">{{arr.constumer}}</td>
              <td>{{ac.name}}物料</td>
              <td>{{ac.daySaleCount}}</td>
              <td>{{ac.daySaleMoney}}</td>
              <td :rowspan="arr.category.length" v-show="idx == 0">{{arr.dayReturnMoney}}</td>
              <td>{{ac.monthSaleCount}}</td>
              <td>{{ac.monthSaleMoney}}</td>
              <td :rowspan="arr.category.length" v-show="idx == 0"> {{arr.monthReturnMoney}}</td>
              <td :rowspan="arr.category.length" v-show="idx == 0">{{arr.dayRemainMoney}}</td>
            </tr>
            <tr style="color:green;font-size: 18px;">
              <td colspan="2">小计</td>
              <td>{{arr.xjdayCount}}</td>
              <td>{{arr.xjdayWeight}}</td>
              <td></td>
              <td>{{arr.xjmonthCount}}</td>
              <td>{{arr.xjmonthWeight}}</td>
              <td></td>
              <td></td>
            </tr>
          </tbody>
        </table>
      </div>
    </el-card>
  </div>
</template>

<script>
/* eslint-disable*/
export default {
  data() {
    return {
      value: '',
      value2: '',
      options: [{
        value: '选项1',
        label: '黄金糕'
      }, {
        value: '选项2',
        label: '双皮奶'
      }, {
        value: '选项3',
        label: '蚵仔煎'
      }, {
        value: '选项4',
        label: '龙须面'
      }, {
        value: '选项5',
        label: '北京烤鸭'
      }],
      pickerOptions: {
        shortcuts: [{
          text: '今日',
          onClick(picker) {
            const end = new Date();
            const start = new Date();
            start.setTime(start.getTime() - 3600 * 1000 * 24 * 1);
            picker.$emit('pick', [start, end]);
          }
        }, {
          text: '最近一周',
          onClick(picker) {
            const end = new Date();
            const start = new Date();
            start.setTime(start.getTime() - 3600 * 1000 * 24 * 7);
            picker.$emit('pick', [start, end]);
          }
        }, {
          text: '最近一个月',
          onClick(picker) {
            const end = new Date();
            const start = new Date();
            start.setTime(start.getTime() - 3600 * 1000 * 24 * 30);
            picker.$emit('pick', [start, end]);
          }
        }, {
          text: '最近三个月',
          onClick(picker) {
            const end = new Date();
            const start = new Date();
            start.setTime(start.getTime() - 3600 * 1000 * 24 * 90);
            picker.$emit('pick', [start, end]);
          }
        }]
      },
      arrList: [],
    }
  },
  methods: {
    getData() {
      return [{
        id: '12987122',
        constumer: '1流川物料公司',
        category: [{
          name: '05',
          daySaleCount: '40',
          daySaleMoney: '1100',
          monthSaleCount: '46',
          monthSaleMoney: '32'
        }, {
          name: '01',
          daySaleCount: '46',
          daySaleMoney: '1600',
          monthSaleCount: '49',
          monthSaleMoney: '1100'
        }, {
          name: '01',
          daySaleCount: '42',
          daySaleMoney: '1200',
          monthSaleCount: '40',
          monthSaleMoney: '1100'
        }, {
          name: '02',
          daySaleCount: '41',
          daySaleMoney: '1100',
          monthSaleCount: '41',
          monthSaleMoney: '1100'
        }],
        dayMetaCount: '169',
        dayMoneyCount: '5000',
        monthMetaCount: '176',
        monthMoneyCount: '3332',
        dayReturnMoney: '37.1',
        monthReturnMoney: '62.1',
        dayRemainMoney: 89,
      }, {
        id: '12987123',
        constumer: '2流川物料公司',
        category: [{
          name: '05',
          daySaleCount: '48',
          daySaleMoney: '1100',
          monthSaleCount: '46',
          monthSaleMoney: '32'
        }, {
          name: '01',
          daySaleCount: '46',
          daySaleMoney: '1600',
          monthSaleCount: '49',
          monthSaleMoney: '1100'
        }, {
          name: '01',
          daySaleCount: '42',
          daySaleMoney: '1200',
          monthSaleCount: '40',
          monthSaleMoney: '1100'
        }],
        dayMetaCount: '136',
        dayMoneyCount: '3900',
        monthMetaCount: '135',
        monthMoneyCount: '2232',
        dayReturnMoney: '12.1',
        monthReturnMoney: '82',
        dayRemainMoney: 41
      }, {
        id: '12987124',
        constumer: '3流川物料公司',
        category: [{
          name: '01',
          daySaleCount: '46',
          daySaleMoney: '1600',
          monthSaleCount: '49',
          monthSaleMoney: '1100'
        }, {
          name: '01',
          daySaleCount: '42',
          daySaleMoney: '1200',
          monthSaleCount: '40',
          monthSaleMoney: '1100'
        }, {
          name: '02',
          daySaleCount: '41',
          daySaleMoney: '1100',
          monthSaleCount: '41',
          monthSaleMoney: '1100'
        }],
        dayMetaCount: '129',
        dayMoneyCount: '3900',
        monthMetaCount: '130',
        monthMoneyCount: '3300',
        dayReturnMoney: '62.6',
        monthReturnMoney: '52',
        dayRemainMoney: 38
      }, {
        id: '12987125',
        constumer: '4流川物料公司',
        category: [{
          name: '05',
          daySaleCount: '48',
          daySaleMoney: '1100',
          monthSaleCount: '46',
          monthSaleMoney: '32'
        }, {
          name: '01',
          daySaleCount: '46',
          daySaleMoney: '1600',
          monthSaleCount: '49',
          monthSaleMoney: '1100'
        }, {
          name: '01',
          daySaleCount: '42',
          daySaleMoney: '1200',
          monthSaleCount: '40',
          monthSaleMoney: '1100'
        }, {
          name: '02',
          daySaleCount: '41',
          daySaleMoney: '1100',
          monthSaleCount: '41',
          monthSaleMoney: '1100'
        }, {
          name: '08',
          daySaleCount: '41',
          daySaleMoney: '1100',
          monthSaleCount: '41',
          monthSaleMoney: '1100'
        }, {
          name: '02',
          daySaleCount: '41',
          daySaleMoney: '1100',
          monthSaleCount: '41',
          monthSaleMoney: '1100'
        }],
        dayMetaCount: '259',
        dayMoneyCount: '7200',
        monthMetaCount: '258',
        monthMoneyCount: '5532',
        dayReturnMoney: '22',
        monthReturnMoney: '32',
        dayRemainMoney: 70
      }, {
        id: '12987126',
        constumer: '5流川物料公司',
        category: [{
          name: '05',
          daySaleCount: '48',
          daySaleMoney: '1100',
          monthSaleCount: '46',
          monthSaleMoney: '32'
        }, {
          name: '01',
          daySaleCount: '46',
          daySaleMoney: '1600',
          monthSaleCount: '49',
          monthSaleMoney: '1100'
        }, {
          name: '01',
          daySaleCount: '42',
          daySaleMoney: '1200',
          monthSaleCount: '40',
          monthSaleMoney: '1100'
        }, {
          name: '02',
          daySaleCount: '41',
          daySaleMoney: '1100',
          monthSaleCount: '41',
          monthSaleMoney: '1100'
        }],
        dayMetaCount: '177',
        dayMoneyCount: '5000',
        monthMetaCount: '176',
        monthMoneyCount: '3332',
        dayReturnMoney: '32.5',
        monthReturnMoney: '78.3',
        dayRemainMoney: 61
      }]
    },
    getDayTonCount() {
      this.arrList.forEach((item) => {
        item.xjdayCount = 0;
        item.xjdayWeight = 0;
        item.xjmonthCount = 0;
        item.xjmonthWeight = 0;
        item.category.forEach((i) => {
          item.xjdayCount += Number(i.daySaleCount);
          item.xjdayWeight += Number(i.daySaleMoney);
          item.xjmonthCount += Number(i.monthSaleCount);
          item.xjmonthWeight += Number(i.monthSaleMoney);
        });
      })
    },
  },
 
  mounted() {
    this.arrList = this.getData();
    this.getDayTonCount();
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.text {
  font-size: 14px;
}

.item {
  margin-bottom: 18px;
}

.clearfix:before,
.clearfix:after {
  display: table;
  content: "";
}

.clearfix:after {
  clear: both
}

td,
th {
  font-style: normal;
  font-weight: normal;
  text-align: center;
}

tr {
  height: 48px;
}


.firstHead th {
  font-size: 14px;
  font-weight: bold;
}

.secondHead th {
  font-size: 13px;
  font-weight: bold;
}

table {
  border-collapse: collapse;
  border-color: #D8DFE6;
}

table thead {
  background: #F3FDFF;
}
</style>
