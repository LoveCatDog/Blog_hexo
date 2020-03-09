---
title: js手写日历
date: 2020-03-09 11:04:38
tags: 
 - Vue
 - javascript
type: tags #（tags,link,categories这三个页面需要配置）
comments: true # (是否需要显示评论，默认true)
description: 'JavaScript手写日历'
top_img: 'https://www.cnblogs.com/skins/codinglife/images/title-yellow.png' #设置顶部图
cover: 'https://th.wallhaven.cc/lg/xl/xl2qgo.jpg'  #缩略图
---
### js手写日历
> 应用场景：移动端签到
  
#### JS代码

![js日历](https://pic.downk.cc/item/5e65b54f98271cb2b8ed960e.png)

```html
<template>
  <div>
    <van-cell-group>
      <van-cell title="签到规则" :value="'本月累计签到天数：' + signDay" />
    </van-cell-group>
    <!-- 日历年月 -->
    <div
      class="bg-white calendar_title"
      style=" display: flex;
    justify-content: space-between;"
    >
      <div>{{year}}年{{month}}月</div>
      <div>
        <van-icon class="margin-right-lg" @click="lastMonth" name="arrow-left" />
        <van-icon @click="nextMonth" name="arrow" />
      </div>
    </div>
    <!-- 日历主体 -->
    <div class="calendar">
      <div class="header">
        <div
          v-for="(dateItem,dateIndex) of date"
          :key="dateIndex"
          :class="{'weekMark':(dateIndex == todayIndex) && isTodayWeek }"
        >
          {{dateItem}}
          <div></div>
        </div>
      </div>
      <div class="date-box">
        <div
          :class="{'nowDay':isToday == item.isToday}"
          v-for="(item,arrIndex) of dateArr"
          :key="arrIndex"
        >
          <div class="date-head" :data-year="year" :data-month="month" :data-datenum="item.dateNum">
            <div class="date-item">
              {{item.dateNum}}
              <div :class="{'checkDay':item.checked}"></div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <van-button
      type="info"
      size="small"
      color="#ff6c6c"
      class="sign_footer_btn"
      @click="hanleToSign"
    >{{singnText}}</van-button>
  </div>
</template>
<script>
export default {
  data() {
    return {
      signDay: 0, //签到天数
      year: 0, //年
      month: 0, //月份
      date: ["日", "一", "二", "三", "四", "五", "六"], //周
      isTodayWeek: false, //当天属于星期几
      todayIndex: 0, //当前属于星期几
      singnText: "签到"
    };
  },
  created() {
    this.getTodayMonth(); //获取当月的签到列表
    this.getList(); //初始化签到数据
  },
  methods: {
    //获取当月的签到列表
    getTodayMonth() {
      let now = new Date();
      let year = now.getFullYear(); //获取当日为某年
      let month = now.getMonth() + 1; //获取当日为某月
      this.year = year;
      this.month = month;
      this.isToday = "" + year + month + now.getDate(); //获取某年某月某日
      this.dateInit(); //初始化日历
    },
    dateInit(setYear, setMonth) {
      let dateArr = []; //需要遍历的日历数组数据
      let arrLen = 0; //dateArr 的数组的长度
      let now = setYear ? new Date(setYear, setMonth) : new Date();
      let year = setYear || now.getFullYear();
      let nextYear = 0;
      let month = setMonth || now.getMonth(); //没有+1方便后面计算当月总天数
      let nextMonth = month + 1 > 11 ? 1 : month + 1;
      let startWeek = new Date(year + "/" + (month + 1) + "/" + 1).getDay(); //目标月1号对应的星期几
      let dayNums = new Date(year, nextMonth, 0).getDate(); //获取目标月有多少天
      let obj = {};
      let num = 0;
      if (month + 1 > 11) {
        //如果月份为13号则年累加1，
        nextYear = year + 1;
        dayNums = new Date(nextYear, nextMonth, 0).getDate(); //获取目标月有多少天
      }
      arrLen = startWeek + dayNums;
      for (let i = 0; i < arrLen; i++) {
        if (i >= startWeek) {
          num = i - startWeek + 1;
          obj = {
            isToday: "" + year + (month + 1) + num,
            dateNum: num,
            weight: 5
          };
        } else {
          obj = {};
        }
        dateArr[i] = obj;
      }
      this.dateArr = dateArr;
      let nowDate = new Date();
      let nowYear = nowDate.getFullYear();
      let nowMonth = nowDate.getMonth() + 1;
      let nowWeek = nowDate.getDay();
      let getYear = setYear || nowYear;
      let getMonth = setMonth >= 0 ? setMonth + 1 : nowMonth;
      if (nowYear == getYear && nowMonth == getMonth) {
        this.isTodayWeek = true;
        this.todayIndex = nowWeek;
      } else {
        this.isTodayWeek = false;
        this.todayIndex = -1;
      }
    },
    getList() {
      var mm = 10;
      if (this.month < 10) {
        mm = `0${this.month}`;
      }
      var date = `${this.year}${mm}`;
      console.log("date", date);
      let list = [
        //某个月的签到列表
        { id: 96830949695488, createTime: 1583718092, credit: 8 },
        {
          id: 92680870551552,
          createTime: 1583464791,
          credit: 8
        }
      ];
      this.signDay = list.length; //获取签到总天数
      let signDay = [];
      for (var i = 0; i < list.length; i++) {
        var newDate = new Date(list[i].createTime * 1000);
        var day = newDate.getDate();
        signDay.push(day);
      }
      console.log("signDay", signDay);
      this.checkData = signDay;
      this.setChecked();
    },

    //已经连续签到的天数：点击事件
    setChecked() {
      let checkData = this.checkData;
      let dateArr = this.dateArr; //获取签到的列表
      for (let i = 0; i < dateArr.length; i++) {
        for (let j = 0; j < checkData.length; j++) {
          if (dateArr[i].dateNum == checkData[j]) {
            dateArr[i]["checked"] = true;
          }
        }
      }
    },
    // 点击按钮去签到
    hanleToSign() {},
    /**
     * 上月切换
     */
    lastMonth() {
      //全部时间的月份都是按0~11基准，显示月份才+1
      let year = this.month - 2 < 0 ? this.year - 1 : this.year;
      let month = this.month - 2 < 0 ? 11 : this.month - 2;
      this.month = month + 1;
      this.year = year;
      this.dateInit(year, month);
      this.getList();
    },
    /**
     * 下月切换
     */
    nextMonth() {
      //全部时间的月份都是按0~11基准，显示月份才+1
      let year = this.month > 11 ? this.year + 1 : this.year;
      let month = this.month > 11 ? 0 : this.month;
      this.month = month + 1;
      this.year = year;
      this.dateInit(year, month);
      this.getList();
    }
  }
};
</script>
<style lang="less" scoped>
/* 日历 */
.sign_footer_btn {
  width: 100%;
  color: rgb(255, 255, 255);
  background: rgb(255, 108, 108);
  border-color: rgb(255, 108, 108);
  position: fixed;
  bottom: 0;
  line-height: 40px;
  height: 40px;
}
.calendar_title {
  padding: 15px;
  font-size: 20px;
}

.calendar_title .icon {
  width: 20px;
  height: 20px;
  margin: 3px auto;
}

.calendar {
  width: 100%;
  background: #fff;
  border-bottom-right-radius: 10px;
  border-bottom-left-radius: 10px;
  padding: 0 0 10px;
  font-family: FZZhunYuan-M02S;
}

.calendar .header {
  margin: 0 auto;
}

.calendar .header > div {
  font-size: 12px;
  display: inline-block;
  width: calc(100% / 7);
  color: #666;
  text-align: center;
  border-bottom: 1px solid #ebedf0;
  padding: 10px 0;
}

.weekMark {
  position: relative;
  width: 80%;
  margin: 0 auto;
}

.weekMark div {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  border-bottom: 2px solid #c8192e;
}

.date-box {
  font-size: 0;
  padding: 5px 0;
  margin: 0 auto;
}

.date-box > div {
  position: relative;
  display: inline-block;
  width: 14.285%;
  color: #000;
  text-align: center;
  vertical-align: middle;
}

.date-head {
  //选中当天日期
  height: 40px;
  font-size: 14px;
}

.date-item {
  margin: 10px 0;
}

.nowDay .date-head {
  color: #c8192e;
  font-size: 17px;
  font-weight: bold;
}

.checkDay {
  background-color: #c8192e;
  height: 5px;
  width: 5px;
  border-radius: 50%;
  margin-left: 25px;
  margin-top: 5px;
}
</style>
```
