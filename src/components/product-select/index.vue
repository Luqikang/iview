<template>
  <Select
    placeholder="请选择商品"
    clearable
    filterable
    :multiple="multiple"
    :value.sync="value"
    @on-change="change">
    <Option
      v-for="item in items"
      :key="item.id"
      :value="item.id">
      {{ item.name }}
    </Option>
  </Select>
</template>

<script>
import Model from '@/models/admin/products'

export default {
  name: 'CProductSelect',
  props: {
    value: {
      type: [String, Number],
      default: 0
    },
    multiple: {
      type: Boolean,
      default: false
    }
  },
  data () {
    return {
      items: []
    }
  },
  async created () {
    this.items = await this.getList()
  },
  methods: {
    async getList () {
      const { data: { items } } = await new Model().GET({
        query: {
          offset: 0,
          limit: 1000
        }
      })

      return items
    },
    change (value) {
      this.$emit('change', value)
    }
  }
}
</script>
