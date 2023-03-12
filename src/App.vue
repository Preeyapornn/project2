
<script setup>
import { ref } from 'vue'

let book = [
  {
    "id":1,
    "title":"Harry",
  },
  {
    "id":2,
    "title":"Conan",
  },
  {
    "id":3,
    "title":"Doramon",
  },
  {
    "id":4,
    "title":"ABC",
  }
]

let history = ref([])
let cart = ref([])
let addButton = ref(false)
let removeButton = ref(false)

function addToCart(event, id) {
  let selectedBook = book.find((item) => item.id === id)
  if (selectedBook && !cart.value.some(item => item.id === selectedBook.id)) {
    cart.value.push(selectedBook)
    history.value.push(selectedBook)
    console.log(cart.value)
  }
}


function removeFromCart(item) {
  let index = cart.value.indexOf(item)
  if (index > -1) {
    cart.value.splice(index, 1)
  }
  console.log(cart.value)
}

</script>

<template>
  <div class="flex justify-center">
    <div class="flex flex-col justify-center">
      <h1>Books for Sale</h1>
      <div>
        <ul>
          <li v-for="item in book" :key="item.id">
            <div class="flex justify-center ">
              {{ item.id }} - {{ item.title }} 
            </div>
            <div class="flex space-x-8">
              <button @click="addToCart($event, item.id)" 
                class="bg-transparent hover:bg-violet-500 text-violet-700 font-semibold hover:text-white py-2 px-4 border border-violet-500 hover:border-transparent rounded">
                Add
              </button>
              <button  @click="removeFromCart(item)"
                class="bg-transparent hover:bg-violet-500 text-violet-700 font-semibold hover:text-white py-2 px-4 border border-violet-500 hover:border-transparent rounded">
                Remove
              </button>
            </div>
          </li>
        </ul>
        <div>
      <p> {{ cart }}</p>
    </div>
      </div>
    </div>
  </div>
</template>
