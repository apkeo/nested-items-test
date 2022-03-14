<template>
  <div class="item">
    <label>Operator</label>
    <input @change="onOperatorInputChange" :value="operator"/>
    <label>Wartość</label>
    <input @change="onTextInputChange" :value="text"/>
  </div>
</template>

<script>
export default {
  props: {
    value: {
      type: Object,
      required: true,
    },
  },
  inheritAttrs: false,
  methods: {
    onTextInputChange(e) {
      this.$emit('valueChange', {
        text: e.target.value,
        operator: this.operator
      })
    },
    onOperatorInputChange(e) {
      this.$emit('valueChange', {
        text: this.text,
        operator: e.target.value
      })
    }
  },
  computed: {
    valueObject() {
      return this.value ? this.value : {}
    },
    text() {
      return this.valueObject.text || ''
    },
    operator() {
      return this.valueObject.operator || ''
    },
  }
}
</script>

<style scoped>
  .item {
    background: black;
    color: white;
    padding: 5px;
  }
</style>