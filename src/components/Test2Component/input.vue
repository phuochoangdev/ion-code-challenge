<template>
  <el-input
    placeholder="Please input"
    :value="internalValue"
    v-on:input="onChange($event)"
    :disabled="disabled"
    :type="typeInput"
    :validate-event="required"></el-input>
</template>
<script>
export default {
  name: 'custom-input',
  props: {
    value: String,
    disabled: Boolean,
    required: Boolean,
    typeInput: {
      type: String,
      default () {
        return 'text'
      }
    }
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
  },
  methods: {
    onChange (e) {
      this.$emit('input', e)
    }
  }
}
</script>
