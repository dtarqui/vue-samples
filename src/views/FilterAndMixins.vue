<template>
  <div class="container">
    <div class="row">
      <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
        <h1>Filters & Mixins</h1>
        <p>Normal text: {{ text }}</p>
        <p>Filter text: {{ text | toUppercases }}</p>
        <p>Filter text: {{ text | to-lowercase }}</p>
        <p>Filter text: {{ text | toUppercases | to-lowercase }}</p>
        <hr />
        <button @click="fruits.push('Berries')">Add New Item</button>
        <hr />
        <input type="text" v-model="filterText" />
        <ul>
          <li v-for="(fruit, index) in filteredFruits" :key="index">{{fruit}}</li>
        </ul>
        <hr />
        <List></List>
      </div>
    </div>
  </div>
</template>

<script>
import List from "../components/FiltersAndMixins/List";
import { fruitMixin } from "../fruitMixin";
export default {
  mixins: [fruitMixin],
  data: () => ({
    text: "Hello There",
  }),
  filters: {
    toUppercases(value) {
      return value.toUpperCase();
    },
  },
  components: {
    List,
  },

};
</script>

<style>
</style>