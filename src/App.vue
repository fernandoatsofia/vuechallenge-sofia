<template>
  <div id="app" class="App">
    <template v-if="loaded">
      <div v-if="loadError">Hubo un error</div>
      <item-list
        v-else
        :data="itemListData"
      ></item-list>
    </template>
  </div>
</template>

<script>
import axios from 'axios';
import ItemList from './ItemList.vue';

export default {
  name: 'app',
  components: {
    ItemList,
  },
  data() {
    return {
      itemListData: null,
      loadError: false,
      loaded: false,
    };
  },
  async mounted() {
    await this.loadItemListData();
  },
  methods: {
    async loadItemListData() {
      try {
        const resp = await axios.get('https://jsonplaceholder.typicode.com/users');
        this.itemListData = resp.data;
      } catch (err) {
        this.loadError = true;
      }
      this.loaded = true;
    },
  },
};
</script>

<style lang="scss">
.App {
  font-family:'Courier New', Courier, monospace;
}
</style>
