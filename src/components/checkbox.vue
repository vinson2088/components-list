<template>
  <div class="checkbox">
    <span v-for="(item, index) in data" :key="index" class="checkbox-box" :class="{check: value.indexOf(index) > -1, button: type === 'button'}">
      <span class="checkbox-simulation" v-if="type === 'point'"><i class="iconfont icon-tick"></i></span>
      <input type="checkbox" :name="'checkbox'+random" :id="'checkbox'+index" class="checkbox-input">
      <label :for="'checkbox'+index" class="checkbox-label" @click="checkboxClick(index)">{{item.label}}</label>
    </span>
  </div>
</template>
<script>
export default {
  props: {
    data: Array,
    value: Array,
    type: {
      type: String,
      default: 'point'
    }
  },
  created() {
    this.random = Math.round(Math.random()*100)
  },
  methods: {
    checkboxClick(num) {
      const index = this.value.indexOf(num)
      let arr = this.value;
      if(index > -1) {
        arr.splice(index, 1)
        this.$emit('input', arr)
      } else {
        arr.push(num);
        arr.sort();
        this.$emit('input', arr)
      }
    }
  },
  data() {
    return {
      random: ''
    }
  }
}
</script>
<style scoped>
.checkbox{
  box-sizing: border-box;
}
.checkbox *{
  box-sizing: inherit;
}
.checkbox-box{
  position: relative;
  margin-left: 5px;
}
.checkbox-simulation{
  white-space: nowrap;
  cursor: pointer;
  outline: none;
  display: inline-block;
  line-height: 1;
  position: relative;
  vertical-align: middle;
  display: inline-block;
  position: relative;
  border: 1px solid #dcdfe6;
  border-radius: 2px;
  box-sizing: border-box;
  width: 14px;
  height: 14px;
  background-color: #fff;
  z-index: 1;
  transition: border-color .25s cubic-bezier(.71,-.46,.29,1.46),background-color .25s cubic-bezier(.71,-.46,.29,1.46);
}
.icon-tick{
  font-size: 12px;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%) scale(0.8);
  color: #fff;
}
.checkbox-input{
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
.checkbox-label{
  margin-left: 5px;
  cursor: pointer;
}
.check .checkbox-simulation{
  border-color: #409eff;
  background: #409eff;
}
.check .checkbox-simulation::after{
  transform: translate(-50%,-50%) scale(1);
}
.check .checkbox-label{
  color: #409eff;
}

.button{
  margin: 0;
}
.button .checkbox-label{
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
.button:first-child .checkbox-label{
  border-left: 1px solid #dcdfe6;
  border-radius: 4px 0 0 4px;
  box-shadow: none!important;
}
.button:last-child .checkbox-label{
  border-radius: 0 4px 4px 0;
}
.check.button .checkbox-label{
  color: #fff;
  background-color: #409eff;
  border-color: #409eff;
  box-shadow: -1px 0 0 0 #409eff;
}
</style>
