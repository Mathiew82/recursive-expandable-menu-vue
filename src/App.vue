<template>
  <div id="app">
    <div class="tac">
      <img alt="Vue logo" src="./assets/logo.png">
    </div>
    <p></p>
    <menu-part-component
      :items="categories"
      :openCategories.sync="openCategories"></menu-part-component>
  </div>
</template>

<script>
import { EventBus } from './event-bus.js';
import MenuPartComponent from './components/MenuPartComponent';

export default {
  name: 'app',
  components: {
    MenuPartComponent
  },
  data() {
    return {
      categories: [
        {
          name: 'Categoría 1',
          subcategories: [
            {
              name: 'Subcategoría 1.1',
              subcategories: [
                {
                  name: 'Subcategoría Hija 1.1.1'
                },
                {
                  name: 'Subcategoría Hija 1.1.2'
                },
                {
                  name: 'Subcategoría Hija 1.1.3'
                }
              ]
            },
            {
              name: 'Subcategoría 1.2',
              subcategories: [
                {
                  name: 'Subcategoría Hija 1.2.1'
                },
                {
                  name: 'Subcategoría Hija 1.2.2'
                },
                {
                  name: 'Subcategoría Hija 1.2.3'
                }
              ]
            },
            {
              name: 'Subcategoría 1.3',
              subcategories: []
            }
          ]
        },
        {
          name: 'Categoría 2',
          subcategories: [
            {
              name: 'Subcategoría 2.1',
              subcategories: [
                {
                  name: 'Subcategoría Hija 2.1.1'
                },
                {
                  name: 'Subcategoría Hija 2.1.2'
                },
                {
                  name: 'Subcategoría Hija 2.1.3'
                }
              ]
            },
            {
              name: 'Subcategoría 2.2',
              subcategories: [
                {
                  name: 'Subcategoría Hija 2.2.1'
                },
                {
                  name: 'Subcategoría Hija 2.2.2'
                },
                {
                  name: 'Subcategoría Hija 2.2.3'
                }
              ]
            },
            {
              name: 'Subcategoría 2.3',
              subcategories: []
            }
          ]
        }
      ],
      openCategories: []
    }
  },
  created() {
    EventBus.$on('toggle-category', category => {
      let findCategory = this.openCategories.find(item => item == category)

      if (!findCategory) {
        this.openCategories.push(category)
      } else {
        let position = this.openCategories.indexOf(category)
        this.openCategories.splice(position, 1)
      }
    })
  }
}
</script>

<style>
body {
  background-color: #222;
  font-family: Arial, "Helvetica Neue", Helvetica, sans-serif;
  padding: 0 20%;
}

.tac {
  text-align: center;
}
</style>
