<template>
  <div :style="{width: '800px', margin: '0 auto'}">
    <div class="row mb-1">
      <p class="col-sm-8">Render a dynamic form.</p>
      <p>More detailed in <strong>readme.md</strong> file</p>
    </div>
    <!--Your code goes here!-->
    <el-form ref="form" :model="form" label-width="120px">
      <el-form-item
        v-for="item in eleForm"
        :key="item.value"
        :label="item.label"
        :rules="{
          required: item.required,
          message: 'Please input ' + item.label,
          trigger: item.valueType.value == 'REFERENCE' && form[item.value] ? 'change' : 'blur'
        }"
        :prop="item.value"
      >
        <keep-alive>
          <component
            v-bind:is="currentComponent[item.valueType.value]"
            v-model="form[item.value]"
            :disabled="item.disabled"
            :required="item.required"
            :typeInput="item.valueType.value == 'LONG' ? 'number' : ''"
            :selectOptionsUrl="selectOptionsUrl[item.value]"></component>
        </keep-alive>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="onSubmit">Submit</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
import CustomInput from './Test2Component/input'
import DatePicker from './Test2Component/datepicker'
import CustomSelect from './Test2Component/custom-select'
const axios = require('axios')

export default {
  name: 'Test3',
  components: {
    CustomInput,
    DatePicker,
    CustomSelect
  },
  data () {
    return {
      eleForm: [],
      form: {},
      selectOptionsUrl: {
        owner: 'http://localhost:3030/modifier',
        modifier: 'http://localhost:3030/owner'
      },
      currentComponent: {
        LONG: CustomInput,
        STRING: CustomInput,
        DATE: DatePicker,
        REFERENCE: CustomSelect
      }
    }
  },
  mounted () {
    axios
      .get('http://localhost:3030/structure')
      .then(response => {
        this.eleForm = [ ...response.data ]
      })
    axios
      .get('http://localhost:3030/data')
      .then(response => {
        const dataFormated = this.formatData(response.data)
        this.form = dataFormated
      })
  },
  methods: {
    onSubmit () {
      console.log(this.form)
      this.$refs.form.validate((valid) => {
        if (valid) {
          alert('submit!')
        } else {
          console.log('error submit!!')
          return false
        }
      })
    },
    formatData (data) {
      for (var property in data) {
        if (property === 'owner' || property === 'modifier') {
          data[property] = data[property].refId
        }
      }

      return data
    }
  }
}
</script>

<style scoped>
  * {
    -webkit-font-smoothing: antialiased;
  }
  *, :after, :before {
    box-sizing: border-box;
  }

</style>
