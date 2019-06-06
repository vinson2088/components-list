<template>
  <div class="radio">
    <span v-for="(item, index) in data" :key="index" class="radio-box" :class="{check: checkList[index], button: type === 'button'}" @click="radioClick(index)">
      <span class="radio-simulation" v-if="type === 'point'"></span>
      <input type="radio" :name="'radio'+random" :id="'radio'+index" class="radio-input">
      <label :for="'radio'+index" class="radio-label">{{item.label}}</label>
    </span>
  </div>
</template>
<script>
export default {
  props: {
    data: Array,
    value: String | Number,
    type: {
      type: String,
      default: 'point'
    }
  },
  created() {
    this.random = Math.round(Math.random()*100)
    this.checkList = this.data.map(() => {
      return false
    });
  },
  methods: {
    radioClick(num) {
      this.checkList = this.checkList.map(() => {
        return false
      })
      this.checkList[num] = true
      this.$emit('input', this.data[num].value)
    }
  },
  data() {
    return {
      random: '',
      checkList: []
    }
  }
}
</script>
<style scoped>
.radio{
  box-sizing: border-box;
}
.radio *{
  box-sizing: inherit;
}
.radio-box{
  position: relative;
  margin-left: 5px;
}
.radio-simulation{
  border: 1px solid #dcdfe6;
  border-radius: 100%;
  width: 14px;
  height: 14px;
  background-color: #fff;
  position: relative;
  cursor: pointer;
  display: inline-block;
  box-sizing: border-box;
}
.radio-simulation::after{
  width: 4px;
  height: 4px;
  border-radius: 100%;
  background-color: #fff;
  content: "";
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%,-50%) scale(0);
  transition: transform .15s ease-in;
}
.radio-input{
  opacity: 0;
  outline: none;
  position: absolute;
  z-index: -1;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  margin: 0;
}
.radio-label{
  margin-left: 5px;
  cursor: pointer;
}
.check .radio-simulation{
  border-color: #409eff;
  background: #409eff;
}
.check .radio-simulation::after{
  transform: translate(-50%,-50%) scale(1);
}
.check .radio-label{
  color: #409eff;
}
.button{
  margin: 0;
}
.button .radio-label{
  position: relative;
  display: inline-block;
  outline: none;
  line-height: 1;
  white-space: nowrap;
  vertical-align: middle;
  background: #fff;
  border: 1px solid #dcdfe6;
  font-weight: 500;
  border-left: 0;
  color: #606266;
  -webkit-appearance: none;
  text-align: center;
  box-sizing: border-box;
  margin: 0;
  cursor: pointer;
  transition: all .3s cubic-bezier(.645,.045,.355,1);
  padding: 12px 20px;
  font-size: 14px;
  border-radius: 0;
}
.button:first-child .radio-label{
  border-left: 1px solid #dcdfe6;
  border-radius: 4px 0 0 4px;
  box-shadow: none!important;
}
.button:last-child .radio-label{
  border-radius: 0 4px 4px 0;
}
.check.button .radio-label{
  color: #fff;
  background-color: #409eff;
  border-color: #409eff;
  box-shadow: -1px 0 0 0 #409eff;
}
</style>
