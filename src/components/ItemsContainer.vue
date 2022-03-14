<template>
  <div class="items-container">
    <h1>Filters:</h1>
    <ItemGroup :value="filterQuery" @valueChange="onChange"></ItemGroup>
  </div>
</template>

<script>
  import ItemGroup from './ItemGroup.vue'

  export default {
    data() {
      return {
        filterQuery: []
      }
    },
    components: {
      ItemGroup,
    },
    methods: {
      onChange(value) {
        this.filterQuery = value
      }
    }
  }
</script>

<style scoped>
.items-container {
  border: 2px solid black;
}
</style>