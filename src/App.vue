<template>
  <div id="app" class="App">
    <template v-if="loaded">
      <div v-if="loadError">Hubo un error</div>
      <item-list
        v-else
        :data="itemListData"
        :sort="sortListData"
      ></item-list>
      <div class="App-btn" @click="sortListData = !sortListData">
        SORT
      </div>
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
      sortListData: false,
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

.App-btn {
  display: inline-block;
  background-color: black;
  color: white;
  padding: 10px 20px;
  user-select: none;
  cursor: pointer;
}
</style>
