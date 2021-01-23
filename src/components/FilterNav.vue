<template>
  <nav class="filter-nav">
    <button @click="updateFilter('all')"
            :class="{active: currentFilter === 'all'}">VIEW ALL</button>
    <span>|</span>
    <button @click="updateFilter('complete')"
            :class="{active: currentFilter === 'complete'}">COMPLETED</button>
    <span>|</span>
    <button @click="updateFilter('incomplete')"
            :class="{active: currentFilter === 'incomplete'}">INCOMPLETE</button>
  </nav>
</template>

<script>
export default {
  name: "FilterNav",
  props: ["currentFilter"],
  methods: {
    updateFilter (filter) {
      this.$emit('filterChange', filter);
    }
  }
}
</script>

<style scoped>

</style>