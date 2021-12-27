<template>
  <nav class="filter-nav">
    <button
      @click="updateFilter('all')"
      :class="{ active: currentFilter === 'all' }"
    >
      View All Projects
    </button>
    <button
      @click="updateFilter('completed')"
      :class="{ active: currentFilter === 'completed' }"
    >
      Completed Projects
    </button>
    <button
      @click="updateFilter('inprogress')"
      :class="{ active: currentFilter === 'inprogress' }"
    >
      Projects in progress
    </button>
  </nav>
</template>

<script>
export default {
  props: ['currentFilter'],
  methods: {
    updateFilter(filterChoice) {
      this.$emit('filterChange', filterChoice);
      //console.log(filterChoice);
    },
  },
};
</script>

<style scoped>
.filter-nav button {
  background: #fff;
  border: none;
  color: #b9c2cc;
  outline: none;
  font-size: 12px;
  text-transform: uppercase;
  margin-right: 10px;
  padding: 10px 10px;
  border-radius: 6px;
  letter-spacing: 1px;
  font-weight: bold;
  cursor: pointer;
  box-shadow: 2px 2px #b9c2cc;
}

.filter-nav button.active {
  color: #30475e;
  box-shadow: 2px 2px #30475e;
}
</style>
