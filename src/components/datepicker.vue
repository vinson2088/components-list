<template>
  <div class="datepicker">
    <div class="picker">
      <label for="datepicker-box">日期：</label>
      <input type="text" readonly="readonly" id="datepicker-box" name="datepicker-box" v-model="selectDate" @click="dropToggle">
      <transition name="slide-fade">
        <div class="dropdown-box" v-show="dropShow">
          <div class="header">
            <div class="left-btn" @click="prevMonth"><i class="iconfont icon-arrow"></i></div>
            <div class="center-txt" @click="backNow">{{year}}年{{month+1}}月</div>
            <div class="right-btn" @click="nextMonth"><i class="iconfont icon-arrow"></i></div>
          </div>
          <div class="body">
            <ul class="date-place">
              <li>星期一</li>
              <li>星期二</li>
              <li>星期三</li>
              <li>星期四</li>
              <li>星期五</li>
              <li>星期六</li>
              <li>星期日</li>
            </ul>
            <ul class="date-place">
              <li v-for="(item, index) in monthList" :key="index"><a href="javascript:void(0)" class="date-item" :class="{active:nowDate === index}" @click="dateClick(index)">{{item}}</a></li>
            </ul>
          </div>
        </div>
      </transition>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    value: Date|String
  },
  created() {
    let date = this.date = new Date();
    this.year = date.getFullYear();
    this.month = date.getMonth();
    this.day = date.getDate();
    this.getMonthList(this.year, this.month);
    if(this.value){
      const chooseDate = this.value;
      let y = chooseDate.getFullYear();
      let m = chooseDate.getMonth() + 1;
      let d = chooseDate.getDate();
      this.selectDate = y + '-' + m + '-' + d
    }
  },
  data() {
    return {
      date: '',
      year: '',
      month: '',
      day: '',
      firstWeek: '',
      lastWeek: '',
      monthList: [],
      selectDate: '',
      dropShow: false,
      nowDate: ''
    }
  },
  methods: {
    backNow() {
      const now = new Date();
      const year = now.getFullYear();
      const month = now.getMonth();
      this.year = year;
      this.month = month;
      this.getMonthList(year, month);
    },
    dropToggle() {
      this.dropShow = !this.dropShow;
    },
    prevMonth(){
      this.month -= 1;
      if(this.month < 0){
        this.month = 11;
        this.year -= 1;
      }
      this.getMonthList(this.year, this.month);
    },
    nextMonth(){
      this.month += 1;
      if(this.month > 11){
        this.month = 0;
        this.year += 1;
      }
      this.getMonthList(this.year, this.month);
    },
    getMonthList(year, month) {
      let firstDay = new Date(year, month, 1);
      this.firstWeek = firstDay.getDay();
      if(this.firstWeek === 0) {
        this.firstWeek = 7
      }
      let lastDay = new Date(year, month+1, 0);
      let monthListLength = lastDay.getDate() + 1;
      let monthList = Object.keys(new Int8Array(monthListLength)).map(Number);
      monthList.shift();
      let lastMonthDate = new Date(year, month, 0);
      const now = new Date();
      this.nowDate = now.getDate() - 1;
      for(let i = 1; i < this.firstWeek; i++){
        let lastMonthDay = lastMonthDate.getDate() + 1 - i
        monthList.unshift(lastMonthDay)
        this.nowDate += 1;
      }
      this.lastWeek = lastDay.getDay();
      let minus = 8 - this.lastWeek;
      if(minus === 8){
        minus = 0;
      }
      for(let j = 1; j < minus; j++){
        monthList.push(j)
      }
      this.monthList = monthList;
      const nowMonth = now.getMonth();
      const nowYear = now.getFullYear();
      if(nowMonth !== month || nowYear !== year){
        this.nowDate = ''
      }
    },
    dateClick(num){
      const day = this.monthList[num];
      let  month = this.month;
      let year = this.year;
      let dayMinus = num - day;
      if(dayMinus > 5) {
        month = this.month + 1
      } else if(dayMinus < -1) {
        month = this.month - 1
      }
      if(month > 11) {
        month = 0;
        year++
      } else if(month < 0){
        month = 11;
        year--
      }
      this.selectDate = year + '-' + (+month+1) + '-' + day;
      const chooseDate = new Date(year, month, day);
      this.dropShow = false;
      this.$emit("input", chooseDate);
    }
  },
}
</script>
<style scoped>
ul,
li{
  list-style: none;
  margin: 0;
  padding: 0;
}
.datepicker{
  box-sizing: border-box;
}
.datepicker *{
  box-sizing: inherit;
}
.picker{
  position: relative;
  display: inline-block;
}
#datepicker-box{
  -webkit-appearance: none;
  background-color: #fff;
  background-image: none;
  border-radius: 4px;
  border: 1px solid #dcdfe6;
  box-sizing: border-box;
  color: #606266;
  display: inline-block;
  font-size: 16px;
  height: 35px;
  line-height: 35px;
  outline: none;
  padding: 0 15px;
  transition: border-color 0.2s cubic-bezier(0.645, 0.045, 0.355, 1);
}
#datepicker-box:focus {
  border-color: #8db0ff;
}
.dropdown-box{
  display: inline-block;
  border: 1px solid #d7d7d7;
  box-shadow: 5px 5px 15px #d7d7d7;
  width: 400px;
  font-size: 12px;
  background-color: #fff;
  border-radius: 5px;
  position: absolute;
  top: calc(100% + 5px);
  left: 0;
  z-index: 9999;
}
.header::after,.date-place::after{
  content: '';
  display: block;
  clear: both;
}
.header .left-btn,.header .right-btn{
  float: left;
  width: 25%;
  padding: 10px 0;
  cursor: pointer;
}
.header .center-txt{
  float: left;
  width: 50%;
  padding: 10px 0;
  cursor: pointer;
}
.header .right-btn{
  transform: rotate(180deg);
}
.date-place li{
  float: left;
  width: 14.2%;
}
.date-item{
  text-decoration: none;
  color: #333;
  display: block;
  padding: 10px 5px;
}
.active{
  background-color: #f0f0f0;
}
.date-item:hover{
  background-color: #e1e1e1;
}
.slide-fade-enter-active{
  transition: all .3s ease;
}
.slide-fade-leave-active{
  transition: all .8s cubic-bezier(1.0, 0.5, 0.5, 1.0)
}
.slide-fade-enter,.slide-fade-leave-to{
  transform: translateY(-10px);
  opacity: 0;
}
</style>
