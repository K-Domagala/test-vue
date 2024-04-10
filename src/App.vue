<script setup lang="ts">
import { ref } from 'vue'
import PageHeader from './components/PageHeader.vue'

//Example products array
const products = ref([
  {id: '33680', description: 'Leyland Contract Matt Brilliant White 10L', priceShown: false},
  {id: '95089', description: 'Leyland Contract Matt Magnolia 10L', priceShown: false},
  {id: '60248', description: 'Leyland Superlaytex Brilliant White 15L', priceShown: false},
  {id: '28311', description: 'Leyland Vinyl Matt 10L Brilliant White', priceShown: false},
  {id: '46152', description: 'Leyland Vinyl Matt 10L Magnolia', priceShown: false},
  {id: '91723', description: 'Leyland Contract Silk 10L Brilliant White', priceShown: false},
  {id: '79281', description: 'Leyland Contract Silk 10L Magnolia', priceShown: false},
  {id: '7129V', description: 'Leyland Magnolia Matt Emulsion 10L', priceShown: false},
  {id: '7291V', description: 'Leyland Pure Brilliant White Matt Emulsion 10L', priceShown: false},
  {id: '422PJ', description: 'Leyland Trade Contract Matt Mercury Grey 10L', priceShown: false}
]);

//Example prices array
const prices = ref([
  {id: '33680', price: '£10.14'},
  {id: '95089', price: '£10.74'},
  {id: '60248', price: '£19.59'},
  {id: '28311', price: '£18.94'},
  {id: '46152', price: '£19.57'},
  {id: '91723', price: '£16.11'},
  {id: '79281', price: '£17.06'},
  {id: '7129V', price: '£8.34'},
  {id: '7291V', price: '£8.12'},
  {id: '422PJ', price: '£10.08'}
])

//Function that will retrieve price of product
const getPrice = (productId: any) => {
  for(let productLine of prices.value){
    if(productLine.id == productId){
      return productLine.price
    }
  }
  return 0;
}

//Function that runs every time a line in a table is clicked. It updates the price of the product and wether it is shown or not
const show = (input: any) => {
  for(let product of products.value){
    if(product.id == input){
      if(!product.price){
        product.price = getPrice(product.id)
      }
      product.priceShown ? product.priceShown = false : product.priceShown = true;
    }
  }
}
</script>

<template>
  <header>
    <PageHeader />
  </header>

  <!-- Table of products -->
  <table class="table-auto w-full p-6 m-6">
    <!-- Table header -->
    <thead class="bg-gray-300">
      <td>
        Product ID
      </td>
      <td>
        Product description
      </td>
    </thead>
    <!-- Table body. Loops through all products in the products array -->
    <tbody>
      <tr v-for="product in products" class="even:bg-blue-300 odd:bg-blue-200 hover:bg-white p-6" @click="show(product.id)">
        <td class="p-2">{{ product.id }}</td>
        <td>
          {{ product.description }}
          <tr>
            <td :hidden="!product.priceShown">Price: {{ product.price }}</td>
          </tr>
        </td>
      </tr>
    </tbody>
  </table>
</template>
