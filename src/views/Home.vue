<template>
  <div class="home">
    <p><myInput :type="type" :label="label" v-model="input"></myInput></p>
    <p><mySelect :label="label" :options="options" v-model="select"></mySelect></p>
    <p><mySwitch v-model="status" :label="label" oncolor="#44cc60" offcolor="#ef5353"></mySwitch></p>
    <p><myProgress percent="50" color="#f00"></myProgress></p>
    <p>
      <myBadge value="12" color="#f00">
        <myButton type="normal">按钮</myButton>
      </myBadge>
    </p>
    <p><myButton type="success">按钮</myButton></p>
  </div>
</template>

<script>
// @ is an alias to /src
import myInput from '@/components/my-input.vue'
import mySelect from '@/components/my-select.vue'
import mySwitch from '@/components/switch.vue'
import myProgress from '@/components/progress.vue'
import myBadge from '@/components/badge.vue'
import myButton from '@/components/button.vue'

export default {
  name: 'home',
  components: {
    myInput,
    mySelect,
    mySwitch,
    myProgress,
    myBadge,
    myButton
  },
  data() {
    return {
      type: 'text',
      label: '标题',
      options: [
        {label: 'txt1', value: 0},
        {label: 'txt2', value: 1},
        {label: 'txt3', value: 2},
        {label: 'txt4', value: 3}
      ],
      input: '',
      select: '',
      status: true,
    }
  },
  methods: {}
}
</script>
<style scoped>
.home{
  font-size: 20px;
}
</style>
