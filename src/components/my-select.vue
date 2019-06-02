<template>
  <div class="select">
    <label>
      <span v-if="label">{{label}}:</span>
    </label>
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
        <i class="iconfont icon-select" :class="{focus: selectFocus}"></i>
      </div>
      <div class="options" v-show="optionsShow">
        <label for="selected">
          <ul>
            <li
              class="options-list"
              v-for="(item, index) in options"
              :key="index"
              @click="optionsListClick(item)"
            >{{item.label}}</li>
          </ul>
        </label>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    label: String,
    options: [Array]
  },
  data() {
    return {
      choose: "",
      selectFocus: false,
      optionsShow: false
    };
  },
  methods: {
    showOptions() {
      this.optionsShow = !this.optionsShow;
      this.selectFocus = !this.selectFocus;
    },
    optionsListClick(item) {
      this.choose = item.label;
      this.$emit("input", item.value);
    }
  }
};
</script>
<style scoped>
ul,
li {
  list-style: none;
  padding: 0;
  margin: 0;
}
.select {
  box-sizing: border-box;
}
.select * {
  box-sizing: inherit;
}
.simulation {
  display: inline-block;
  position: relative;
  margin-left: 15px;
}
.select-box {
  position: relative;
}
.iconfont {
  position: absolute;
  right: 5px;
  top: 0;
  height: 100%;
  transform: rotate(180deg);
  transition: transform 0.3s;
}
.iconfont:before {
  display: inline-block;
  vertical-align: middle;
}
.iconfont:after {
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
  font-size: inherit;
  height: 40px;
  line-height: 40px;
  outline: none;
  padding: 0 15px;
  transition: border-color 0.2s cubic-bezier(0.645, 0.045, 0.355, 1);
  width: 100%;
  font-size: 16px;
  padding-right: 5px;
  cursor: pointer;
}
.selected:focus {
  border-color: #8db0ff;
}
.options {
  position: absolute;
  top: calc(100% + 5px);
  border: 1px solid #dcdfe6;
  box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  min-width: 100%;
  z-index: 9999;
}
.options-list {
  font-size: 14px;
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
</style>
<style scoped>
@import url(../assets/iconfont/iconfont.css);
</style>
