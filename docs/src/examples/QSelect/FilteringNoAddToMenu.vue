<template>
  <div class="q-pa-md">
    <q-select
      filled
      v-model="modelFilter"
      use-input
      use-chips
      multiple
      input-debounce="0"
      @new-value="filterCreateValue"
      :options="filterOptions"
      @filter="filterFn"
      style="width: 250px"
    />
  </div>
</template>

<script>
const stringOptions = [
  'Google', 'Facebook', 'Twitter', 'Apple', 'Oracle'
]

export default {
  data () {
    return {
      model: null,
      modelFilter: null,

      filterOptions: stringOptions
    }
  },

  methods: {
    filterCreateValue (val, done) {
      if (val.length > 2) {
        if (!stringOptions.includes(val)) {
          done(val)
        }
        else {
          done()
        }
      }
    },

    filterFn (val, update) {
      let self = this
      update(() => {
        if (val === '') {
          this.filterOptions = stringOptions
        }
        else {
          const needle = val.toLowerCase()
          self.filterOptions = stringOptions.filter(v => v.toLowerCase().indexOf(needle) > -1)
        }
      })
    }
  }
}
</script>
