<template>
  <div :style="{width: '800px', margin: '0 auto'}">
    <div class="row mb-1">
      <p class="col-sm-8">Implement <strong>input</strong>, <strong>datepicker</strong>, and <strong>select/dropdown</strong> knowing that these component get initial data from server and be able to retrieve new data as user change it.</p>
      <p>Use <a href="http://element.eleme.io/?ref=madewithvuejs.com#/en-US" target="_blank">this</a> library</p>
    </div>
    <div class="row mb-1">
      <p>Custom Input</p>
      <CustomInput v-model="inputData" />
    </div>
    <div class="row mb-1">
      <p>Custom Datepicker</p>
      <DatePicker v-model="dateData" />
    </div>
    <div class="row mb-1">
      <p class="color-picker__label">Custom Colorpicker</p>
      <ColorPicker :value="color" />
    </div>
    <div class="row mb-1">
      <p>Custom Select</p>
      <CustomSelect :selectOptions="selectOptions" v-model="selectValue" />
    </div>
  </div>
</template>

<script>
import CustomInput from './Test2Component/input'
import DatePicker from './Test2Component/datepicker'
import ColorPicker from './Test2Component/colorpicker'
import CustomSelect from './Test2Component/custom-select'
const axios = require('axios')

export default {
  name: 'Test2',
  components: {
    CustomInput,
    DatePicker,
    ColorPicker,
    CustomSelect
  },
  data () {
    return {
      inputData: '',
      dateData: '',
      color: '',
      selectOptions: [],
      selectValue: ''
    }
  },
  mounted () {
    setTimeout(() => {
      this.inputData = 'This is initial data.'
      this.dateData = '1551693570892'
      this.color = '#cdcdcd'
    }, 900)
    axios
      .get('http://localhost:3030/modifier')
      .then(response => {
        this.selectOptions = [ ...response.data.items ]
      })
  },
  methods: {
    handleChangeData (newValue) {
      console.log('new Value', newValue)
    }
  }
}
</script>

<style scoped>
  .mb-1, .my-1 {
    margin-bottom: 4px!important;
    margin-bottom: .25rem!important;
  }
  .row {
    display: -ms-flexbox;
    display: flex;
    -ms-flex-wrap: wrap;
    flex-wrap: wrap;
    margin-right: -15px;
    margin-left: -15px;
  }
  .col-sm-2 {
     -ms-flex: 0 0 16.666667%;
     flex: 0 0 16.666667%;
     max-width: 16.666667%;
   }
  .col-sm-2, .col-sm-10 {
    position: relative;
    width: 100%;
    min-height: 1px;
    padding-right: 15px;
    padding-left: 15px;
  }
  .pt-1, .py-1 {
    padding-top: 4px!important;
    padding-top: .25rem!important;
  }
  .col-sm-10 {
    -ms-flex: 0 0 83.333333%;
    flex: 0 0 83.333333%;
    max-width: 83.333333%;
  }
  .progress, .progress-bar {
    display: -ms-flexbox;
    display: flex;
  }
  .progress {
    height: 16px;
    height: 1rem;
    overflow: hidden;
    font-size: 12px;
    font-size: .75rem;
    background-color: #e9ecef;
    border-radius: .25rem;
  }
  .progress-bar {
    -ms-flex-direction: column;
    flex-direction: column;
    -ms-flex-pack: center;
    justify-content: center;
    color: #fff;
    text-align: center;
    white-space: nowrap;
    background-color: #007bff;
    transition: width .6s ease;
  }
  .progress, .progress-bar {
    display: -ms-flexbox;
    display: flex;
  }
  * {
    -webkit-font-smoothing: antialiased;
  }
  *, :after, :before {
    box-sizing: border-box;
  }
  .color-picker__label {
    margin-right: 10px;
  }
</style>
