<template>
  <div class="pagination">
    <span>共{{total}}条</span>
    <div class="simulation">
      <div class="select-box" @click="showOptions">
        <input
          type="text"
          readonly="readonly"
          class="selected"
          v-model="choose"
          autocomplete="off"
          placeholder="请选择"
          id="selected"
        >
        <i class="iconfont icon-select triangle" :class="{focus: selectFocus}"></i>
      </div>
      <transition name="slide-fade">
        <div class="options" v-show="optionsShow">
          <ul class="options-box">
            <li
              class="options-list"
              v-for="(item, index) in options"
              :key="index"
              @click="optionsListClick(item)"
            >{{item.label}}</li>
          </ul>
        </div>
      </transition>
    </div>
    <span class="Btn" @click="currentBack" v-show="begin"><i class="iconfont icon-arrow"></i></span>
    <ul class="pageList">
      <li v-for="(item, index) in pageList" :key="index" class="Btn" :class="{active: item.current}" @click="pageClick(item.label)">{{item.label}}</li>
    </ul>
    <span class="Btn arrow-right" @click="currentIncrease" v-show="last"><i class="iconfont icon-arrow"></i></span>
  </div>
</template>
<script>
import mySelect from './my-select.vue'
export default {
  components: {
    mySelect
  },
  props: {
    total: Number,
    value: {
      type: Number,
      default: 1
    },
    pagenumber: Number
  },
  data() {
    return {
      options: [
        {label: '10条/页', value: 10},
        {label: '20条/页', value: 20},
        {label: '50条/页', value: 50},
        {label: '100条/页', value: 100}
      ],
      select: '',
      selectFocus: false,
      optionsShow: false,
      choose: '10条/页',
      begin: true,
      last: true
    }
  },
  computed: {
    pageList() {
      let lastPage = Math.round(this.total / this.pagenumber);
      this.begin = true;
      this.last = true;
      if(this.value === 1){
        this.begin = false
      } else if(this.value === lastPage) {
        this.last = false
      }
      let currentPage = {label: this.value, current: true};
      let arr = [];
      arr.push(currentPage)
      let owe = 0;
      let owe2 = 0
      for(let j = 0; j < 2; j++) {
        let num = this.value - j - 1;
        if(num > 0) {
          let obj = {label: num, current: false}
          arr.unshift(obj)
        } else {
          owe++
        }
      }
      for(let z = 0; z < (2 + owe); z++) {
        let num = this.value + z + 1;
        if(num < lastPage+1){
          let obj2 = {label: num, current: false}
          arr.push(obj2)
        } else {
          owe2++
        }
      }
      for(let i = 0; i < owe2; i++) {
        let num = arr[0].label - 1
        let obj = {label: num, current: false}
        arr.unshift(obj)
      }
      return arr
    }
  },
  methods: {
    currentBack() {
      let newCurrent = this.value - 1;
      this.$emit('input', newCurrent)
    },
    currentIncrease() {
      let newCurrent = this.value + 1;
      this.$emit('input', newCurrent)
    },
    showOptions() {
      this.optionsShow = !this.optionsShow;
      this.selectFocus = !this.selectFocus;
    },
    optionsListClick(item) {
      this.choose = item.label;
      this.optionsShow = false;
      this.selectFocus = false;
    },
    pageClick(number) {
      if(typeof(number) === 'number'){
        this.$emit('input', number)
      }
    }
  },
}
</script>
<style scoped>
@import url(./../assets/iconfont/iconfont.css);
ul,li{
  list-style: none;
  padding: 0;
  margin: 0;
}
.pagination{
  box-sizing: border-box;
  font-size: 12px;
}
.pagination *{
  box-sizing: inherit;
}
.simulation {
  display: inline-block;
  position: relative;
  margin-left: 15px;
  width: 88px;
}
.select-box {
  position: relative;
}
.triangle {
  position: absolute;
  right: 5px;
  top: 0;
  height: 100%;
  transform: rotate(180deg);
  transition: transform 0.3s;
}
.triangle:before {
  display: inline-block;
  vertical-align: middle;
}
.triangle:after {
  content: "";
  display: inline-block;
  vertical-align: middle;
  height: 100%;
}
.focus {
  transform: rotate(0deg);
}
.selected {
  background-color: #fff;
  background-image: none;
  border-radius: 4px;
  border: 1px solid #dcdfe6;
  box-sizing: border-box;
  color: #606266;
  display: inline-block;
  height: 30px;
  line-height: 30px;
  outline: none;
  padding: 0 8px;
  transition: border-color 0.2s cubic-bezier(0.645, 0.045, 0.355, 1);
  width: 100%;
  font-size: 12px;
  padding-right: 5px;
  cursor: pointer;
}
.selected:focus {
  border-color: #8db0ff;
}
.options {
  position: absolute;
  display: inline-block;
  top: calc(100% + 5px);
  left: 0;
  border: 1px solid #dcdfe6;
  box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  min-width: 100%;
  z-index: 9999;
}
.options-box{
  background-color: #fff;
}
.options-list {
  font-size: 12px;
  padding: 0 20px;
  position: relative;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  color: #606266;
  height: 34px;
  line-height: 34px;
  box-sizing: border-box;
  cursor: pointer;
  text-align: left;
}
.options-list:hover {
  background-color: #f5f7fa;
}
.pageList{
  display: inline-block;
}
.Btn{
  display: inline-block;
  vertical-align: middle;
  width: 40px;
  height: 30px;
  line-height: 30px;
  text-decoration: none;
  color: #333;
  cursor: pointer;
  border: 1px solid #d7d7d7;
  margin: 0 5px;
}
.Btn.active{
  color: #fff;
  background-color: #6d9aff;
}
.arrow-right{
  transform: rotate(180deg);
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
