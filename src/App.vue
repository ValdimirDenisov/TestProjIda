<template>
  <div id="app">
    <Second>
      <h1 class="text">Добавление товара</h1>
      <AddForm @addProduct="addNewProduct($event)"></AddForm>
    </Second>
    <Main>
      <Sorter @changeSort="sortProducts($event)"></Sorter>
      <Product v-for="item in products" :key="item['name']" :config="item" @deleteItem="deleteProduct($event)"></Product>
    </Main>
  </div>
</template>

<script>

import AddForm from './components/ProductAddForm'
import Product from './components/Product'
import Second from './components/SecondContainer'
import Main from './components/MainContainer'
import Sorter from './components/SortSelect'

export default {
  name: 'App',
  components: {
    AddForm,
    Product,
    Main,
    Second,
    Sorter
  },
  data() {
    return {
      products: [
        {
          'id': 0,
          'name': 'Наименование товара',
          'description': 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
          'price': '10 000',
          'src': 'https://s3-alpha-sig.figma.com/img/488b/7f1f/e88ef4c6003a678c0c9d6a1b91606ae9?Expires=1629072000&Signature=E3eze9iRhyf7paZmC8jEXYhl9tQFBbqFqE96mKB6NberSlLMBc7NM9NUqvPKfD2GKJsU8Err37~M~qY2mG~2lTFcQnnn0q~lrcW8MM4X--YMzvRrBy6nWm29OFg~xgJnX-fhomRBMR-if2QGRG1uzrBrtj82doY4q2cMq13KRXqJBMOxZ9J5lT4yNExwjUftaYv5rgfYx9CjIgZszvL1phAjhZjox0cx1Gglu6lkOunXbqVhZtPan3ve~n~BQ4j2CAQO3Ll1kdehb6YD4vjh-ZEimMdl2iQQfFevcGIsZAjG9cUA~RngtA89-UY4fev1qIlzVoMsEJaMosdTLe4qDQ__&Key-Pair-Id=APKAINTVSUGEWH5XD5UA'
        },
        {
          'id': 1,
          'name': 'Наименование товара',
          'description': 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
          'price': '10 000',
          'src': 'https://s3-alpha-sig.figma.com/img/488b/7f1f/e88ef4c6003a678c0c9d6a1b91606ae9?Expires=1629072000&Signature=E3eze9iRhyf7paZmC8jEXYhl9tQFBbqFqE96mKB6NberSlLMBc7NM9NUqvPKfD2GKJsU8Err37~M~qY2mG~2lTFcQnnn0q~lrcW8MM4X--YMzvRrBy6nWm29OFg~xgJnX-fhomRBMR-if2QGRG1uzrBrtj82doY4q2cMq13KRXqJBMOxZ9J5lT4yNExwjUftaYv5rgfYx9CjIgZszvL1phAjhZjox0cx1Gglu6lkOunXbqVhZtPan3ve~n~BQ4j2CAQO3Ll1kdehb6YD4vjh-ZEimMdl2iQQfFevcGIsZAjG9cUA~RngtA89-UY4fev1qIlzVoMsEJaMosdTLe4qDQ__&Key-Pair-Id=APKAINTVSUGEWH5XD5UA'
        }
      ],
      sortType: 0
    }
  },
  watch: {
    products: function () {
      localStorage.setItem('storedProducts', JSON.stringify(this.products))
    },

  },
  methods: {
    addNewProduct(product) {
      let maxId = -122
      this.products.forEach((item) => {
        if (maxId < item['id']) {
          maxId = item['id']
        }
      })
      product['id'] = maxId + 1
      this.products.push(product)
    },
    deleteProduct(a) {
      let newProducts = []
      this.products.forEach((item) => {
        if (item['id'] !== a) {
          newProducts.push(item)
        }
      })
      this.products = newProducts
    },
    sortProducts(sortType) {
      let defaultSort = (a, b) => {
        return a['id'] - b['id']
      }
      let priceAscendingSort = (a, b) => {
        return +a['price'].replace(/\s+/g, '') - +b['price'].replace(/\s+/g, '')
      }
      let priceDescendingSort =  (a, b) => {
        return +b['price'].replace(/\s+/g, '') - +a['price'].replace(/\s+/g, '')
      }
      let nameSort = (a, b) => {
        if (a['name'] > b['name']) {
          return 1;
        }
        if (a['name'] < b['name']) {
          return -1;
        }
        return 0;
      }
      switch (sortType) {
        case '0':
          this.products.sort(defaultSort)
          break
        case '1':
          this.products.sort(priceAscendingSort)
          break
        case '2':
          this.products.sort(priceDescendingSort)
          break
        case '3':
          this.products.sort(nameSort)
          break
      }
    }
  },
  mounted() {
    if (localStorage.storedProducts) {
      this.products = JSON.parse(localStorage.storedProducts);
    }
  }
}
</script>

<style lang="sass">
#app
  display: flex
  flex-wrap: wrap
  font-family: Source Sans Pro, sans-serif

  body
    background-color: #FFFEFBCC

.text
  //font-family: Source Sans Pro
  font-size: 28px
  font-style: normal
  font-weight: 600
  line-height: 35px
  letter-spacing: 0em
  text-align: center


</style>
