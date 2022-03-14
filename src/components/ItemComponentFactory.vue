<template>
  <Component :is="componentName" :value="value" @valueChange="onChange"/>
</template>

<script>
  import { defineAsyncComponent } from 'vue'
  import {typeToComponentMap} from './typeToComponentMap'
  const Item = defineAsyncComponent(() => import('./Item.vue'))
  const ItemGroup = defineAsyncComponent(() => import('./ItemGroup.vue'))

  export default {
    props: {
      value: {
        type: null,
        required: true,
      },
      type: {
        type: String,
        required: true,
      }
    },
    methods: {
      onChange(e) {
        this.$emit('valueChange', e)
      }
    },
    components: {
      Item,
      ItemGroup,
    },
    computed: {
      componentName() {
        return typeToComponentMap.get(this.type)
      }
    }
  }
</script>