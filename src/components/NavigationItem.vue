<template>
    <a class="item" v-bind:class="{ selected: selected }"
       @click="handleItemClick(city.id)">
      {{ city.name }}, {{ city.country }}
    </a>
</template>

<script>
export default {
  name: 'NavigationItem',
  props: {
    city: Object,
    selected: Boolean,
  },
  methods: {
    handleItemClick(cityId) {
      this.$emit('selectCity', cityId);
    },
  },
};
</script>

<style scoped>
.item {
  padding: 8px 16px;
}
.item:hover {
  cursor: pointer;
  background-color: lightgray;
}
.item.selected {
  background-color: lightgray;
}
</style>
