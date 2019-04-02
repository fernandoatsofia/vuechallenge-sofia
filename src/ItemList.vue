<template>
  <ul class="ItemList">
    <li
      v-for="item in sortedData"
      :key="item.id"
      class="ItemList-item"
    >
      <p>
        <b>Name:</b> {{ item.name }}
      </p>
    </li>
  </ul>
</template>

<script>
export default {
  name: 'ItemList',
  props: {
    data: {
      required: true,
      type: Array,
    },
  },
  computed: {
    sortedData() {
      const { data } = this;
      return data.sort((a, b) => {
        const nameA = a.name.toUpperCase(); // ignore upper and lowercase
        const nameB = b.name.toUpperCase(); // ignore upper and lowercase
        if (nameA < nameB) {
          return -1;
        }
        if (nameA > nameB) {
          return 1;
        }
        // names must be equal
        return 0;
      });
    },
  },
};
</script>

<style>
.ItemList {
  padding: 10px;
  list-style-type: none;
}
</style>
