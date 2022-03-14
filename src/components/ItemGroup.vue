<template>
  <div class="item-group">
    <div class="header">
      <button @click="$emit('delete')">Delete group</button>
      <button @click="add('group')">Add group</button>
      <button @click="add('item')">Add item</button>
    </div>
    <div class="items">
      {{JSON.stringify(value)}}
      <ItemComponentFactory v-for="(item, i) in items" :value="item.value" :type="item.type" :key="i" @valueChange="onChildChange(i, $event)"/>
    </div>
  </div>
</template>

<script>
  import ItemComponentFactory from './ItemComponentFactory.vue'

  export default {
    props: {
      value: {
        type: null,
        required: true,
      }
    },
    computed: {
      items() {
        if(!this.value) {
          return []
        }
        if(!this.value) {
          return []
        }
        return this.value
      },
    },
    components: {
      ItemComponentFactory,
    },
    methods: {
      add(type) {
        this.$emit('valueChange', [
          ...(this.value || []),
          {
            type,
          }
        ])
      },
      onChildChange(index, value) {
        const newValue = this.value.map((e, i) => {
          if(i !== index) {
            return e
          }
          return {
            type: e.type,
            value,
          }
        })
        this.$emit('valueChange', newValue)
      }
    }
  }
</script>

<style scoped>
  .item-group {
    background: hsl(0deg 0% 0% / 3%);
    border-left: 2px solid midnightblue;
    border-bottom: 2px solid midnightblue;
  }

  .header {
    background: midnightblue;
    color: white;
    padding: 5px;
    display: flex;
    gap: 5px;
  }

  button {
    background: darkorange;
    color: black;
    border: none;
  }

  .items {
    background: hsl(0deg 0% 0% / 3%);
    padding: 15px;
    display: flex;
    flex-direction: column;
    gap: 10px;
  }
</style>