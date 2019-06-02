<template>
  <div class="switch">
    <label v-if="label">{{label}}</label>
    <div
      class="switch-box"
      :class="{on: value}"
      @click="switchClick"
      :style="{backgroundColor: bgColor}"
    >
      <div class="btn"></div>
      <input type="checkbox" name="switch-input" id="switch-input" v-model="value">
    </div>
  </div>
</template>
<script>
export default {
  props: {
    value: {
      type: Boolean,
      default: false
    },
    label: String,
    oncolor: String,
    offcolor: String
  },
  data() {
    return {};
  },
  computed: {
    bgColor() {
      if (this.value) {
        return this.oncolor;
      } else {
        return this.offcolor;
      }
    }
  },
  methods: {
    switchClick() {
      this.$emit("input", !this.value);
    }
  }
};
</script>
<style scoped>
.switch {
  box-sizing: border-box;
}
.switch * {
  box-sizing: inherit;
}
.switch-box {
  width: 50px;
  display: inline-block;
  border-radius: 50px;
  height: 25px;
  cursor: pointer;
  text-align: left;
  transition: all 0.3s;
  margin-left: 5px;
}
.on .btn {
  margin-left: calc(100% - 24px);
}
.btn {
  width: 24px;
  height: 24px;
  background-color: #fff;
  border-radius: 50px;
  display: inline-block;
  vertical-align: middle;
  transition: all 0.3s;
}
.switch-box::after {
  content: "";
  height: 100%;
  display: inline-block;
  vertical-align: middle;
}
#switch-input {
  display: none;
}
</style>
