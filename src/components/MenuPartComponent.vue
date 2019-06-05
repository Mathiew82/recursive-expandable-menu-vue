<template>
  <ul>
    <li
      v-for="item in items"
      :key="item.name"
      :class="{ 'show' : findCategory(item) }">
      <span
        v-if="item.childs && item.childs.length"
        @click="toggleChilds(item)">
        <template v-if="!findCategory(item)">
          +
        </template>
        <template v-else>
          -
        </template>
      </span>
      {{ item.name }}
      <menu-part-component
        v-if="item.childs && item.childs.length"
        :items="item.childs"
        :openCategories.sync="openCategories"></menu-part-component>
    </li>
  </ul>
</template>

<script>
import { EventBus } from '../event-bus.js';

export default {
  name: 'MenuPartComponent',
  props: {
    items: {
      type: Array,
      required: true
    },
    openCategories: {
      type: Array,
      required: true
    }
  },
  methods: {
    toggleChilds(category) {
      EventBus.$emit('toggle-category', category)
    },
    findCategory(category) {
      return this.openCategories.find(item => item == category)
    }
  }
}
</script>

<style>
ul {
  list-style-type: none;
  list-style-position: inside;
  margin: 0;
  padding: 0;
}

li {
  height: 30px;
  line-height: 30px;
  color: white;
  display: block;
  overflow: hidden;
  padding: 0 20px 0 26px;
  position: relative;
  text-align: left;
}

li.show {
  height: auto;
}

li > span {
  width: 18px;
  height: 24px;
  background-color: #f0f0f0;
  border: 1px solid grey;
  color: black;
  display: block;
  padding: 0;
  position: absolute;
  top: 0;
  left: 0;
  text-align: center;
}

li > span:hover {
  background-color: #e0e0e0;
  cursor: pointer;
}

ul > li > ul > li {
    display: block;
    padding: 0 30px 0 26px;
}

ul > li > ul > li > ul > li {
    display: block;
    padding: 0 40px 0 26px;
}
</style>
