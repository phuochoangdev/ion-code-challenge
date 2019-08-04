<template>
  <el-select
    :value="value"
    v-on:change="onChange($event)"
    placeholder="Select"
    class="select"
    :disabled="disabled"
  >
    <el-option
      v-for="option in options"
      :key="option.refId"
      :label="option.label"
      :value="option.value">
    </el-option>
  </el-select>
</template>
<script>
const axios = require('axios')

export default {
  name: 'custom-select',
  props: {
    selectOptionsUrl: String,
    value: String,
    disabled: Boolean,
    required: Boolean
  },
  data () {
    return {
      options: []
    }
  },
  created () {
    axios
      .get(this.selectOptionsUrl)
      .then(response => {
        this.options = [ ...response.data.items ]
      })
  },
  methods: {
    onChange (e) {
      this.$emit('input', e)
    }
  }
}
</script>
<style scoped>
  .el-select {
    width: 100%;
  }
</style>
