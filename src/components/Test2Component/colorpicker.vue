<template>
  <el-color-picker v-model="internalValue"></el-color-picker>
</template>
<script>
export default {
  name: 'color-picker',
  props: {
    value: String
  },
  data () {
    return {
      internalValue: this.value
    }
  },
  watch: {
    value () {
      this.internalValue = this.value
    }
  }
}
</script>
