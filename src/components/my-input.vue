<template>
  <div class="input">
    <label for="my-input">
      <span v-if="label">{{label}}:</span>
    </label>
    <div class="simulation">
      <input :type="type" id="my-input" name="my-input" @input="handleInput" v-model="value">
    </div>
  </div>
</template>
<script>
export default {
  props: {
    type: String,
    label: String
  },
  data() {
    return {
      value: ""
    };
  },
  methods: {
    handleInput(event) {
      const value = event.target.value;
      this.$emit("input", value);
    }
  }
};
</script>
<style scoped>
.input {
  box-sizing: border-box;
}
.input * {
  box-sizing: inherit;
}
.simulation {
  display: inline-block;
  margin-left: 15px;
}
#my-input {
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
  width: 100%;
}
#my-input:focus {
  border-color: #8db0ff;
}
</style>
