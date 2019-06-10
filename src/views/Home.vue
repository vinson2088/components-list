<template>
  <div class="home">
    <p><myInput :type="type" :label="label" v-model="input"></myInput></p>
    <p><mySelect :label="label" :options="options" v-model="select"></mySelect></p>
    <p><mySwitch v-model="status" :label="label" oncolor="#44cc60" offcolor="#ef5353"></mySwitch></p>
    <p><myProgress percent="50" color="#59abff"></myProgress></p>
    <p>
      <myBadge value="12" color="#f00">
        <myButton type="normal" size="middle">按钮</myButton>
      </myBadge>
    </p>
    <p><myButton type="success" size="middle">按钮</myButton></p>
    <p><myDatepicker v-model="selectDate"></myDatepicker></p>
    <p><mySlider color="#0f0" width="300" v-model="percent"></mySlider></p>
    <p><myPagination @sizeChange="sizeChange" :total='total' v-model="current" :pagenumber="pagenumber" :sizeArr="sizeArr"></myPagination></p>
    <p><myImgBlock :data="imgBlockData" column="3"></myImgBlock></p>
    <p><myRadio :data="radioList" v-model="radio" type="point"></myRadio></p>
    <p><myCheckbox :data="checkboxList" v-model="checkbox" type="button"></myCheckbox></p>
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
import myDatepicker from '@/components/datepicker.vue'
import mySlider from '@/components/slider.vue'
import myPagination from '@/components/pagination.vue'
import myImgBlock from '@/components/imgBlock.vue'
import myRadio from '@/components/radio.vue'
import myCheckbox from '@/components/checkbox.vue'

export default {
  name: 'home',
  components: {
    myInput,
    mySelect,
    mySwitch,
    myProgress,
    myBadge,
    myButton,
    myDatepicker,
    mySlider,
    myPagination,
    myImgBlock,
    myRadio,
    myCheckbox
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
      input: '123',
      select: 1,
      status: false,
      selectDate: '',
      tableData: [
        {label: '123', value: 1},
        {label: '123', value: 1},
        {label: '123', value: 1},
        {label: '123', value: 1}
      ],
      percent: 90,
      total: 105,
      current: 1,
      pagenumber: 10,
      sizeArr: [20, 40, 60, 80],
      imgBlockData: [
        {img: require('./../assets/logo.png'), alt: '图片描述', text: '这是一条消息', link: 'https://www.google.com'},
        {img: require('./../assets/logo.png'), alt: '图片描述', text: '这是一条消息', link: 'https://www.baidu.com'},
        {img: require('./../assets/logo.png'), alt: '图片描述', text: '这是一条消息', link: 'https://cn.bing.com/'}
      ],
      radioList: [
        {label: '选项一', value: 4},
        {label: '选项二', value: 6},
        {label: '选项三', value: 9},
        {label: '选项四', value: 0}
      ],
      radio: '',
      checkboxList: [
        {label: '选项一', value: 1},
        {label: '选项二', value: 2},
        {label: '选项三', value: 3},
        {label: '选项四', value: 4}
      ],
      checkbox: []
    }
  },
  methods: {
    sizeChange(num) {
      this.pagenumber = num;
    },
  }
}
</script>
<style scoped>
.home{
  font-size: 20px;
}
</style>
