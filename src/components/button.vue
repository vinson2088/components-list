<template>
  <div class="button" :class="[typeClass, size]">
    <slot></slot>
  </div>
</template>
<script>
export default {
  props: {
    type: String,
    size: {
      type: String,
      validator (value) {
        let arr = ['big', 'middle', 'small']
        if(arr.indexOf(value) > -1){
          return value
        } else {
          throw "button type格式错误"
        }
      },
      default: "middle"
    }
  },
  data() {
    return {};
  },
  computed: {
    typeClass() {
      return this.type;
    }
  }
};
</script>
<style scoped>
.button {
  box-sizing: border-box;
  border: 1px solid;
  color: #fff;
  display: inline-block;
  border-radius: 5px;
  cursor: pointer;
}
.button * {
  box-sizing: inherit;
}
.normal {
  background-color: #fff;
  border-color: #fff;
  color: #333;
  border-color: #d7d7d7;
}
.normal:active {
  background-color: #e1e1e1;
}
.success {
  background-color: #47dd81;
  border-color: #47dd81;
}
.success:hover {
  background-color: #64e294;
}
.success:active {
  background-color: #27c463;
}
.info {
  background-color: #4ba7f3;
  border-color: #4ba7f3;
}
.info:hover {
  background-color: #6ab9fa;
}
.info:active {
  background-color: #4995d4;
}
.warning {
  background-color: #e6ab65;
  border-color: #e6ab65;
}
.warning:hover {
  background-color: #f3c081;
}
.warning:active {
  background-color: #d09b5d;
}
.danger {
  background-color: #e85e5e;
  border-color: #e85e5e;
}
.danger:hover {
  background-color: #fa7979;
}
.danger:active {
  background-color: #ca5151;
}
.big {
  padding: 10px 20px;
  font-size: 22px;
}
.middle {
  padding: 5px 10px;
  font-size: 14px;
}
.small {
  padding: 2px 5px;
  font-size: 12px;
}
</style>
