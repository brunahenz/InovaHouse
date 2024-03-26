<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'
const casas = ref([])

onMounted(async () => {
  const response = await axios.get('https://fakestoreapi.com/products')
  casas.value = response.data
})

const formatPrice = (price) => `R$ ${price.toFixed(2).replace('.', ',')}`
</script>

<template>
  <div>
    <h1 class="title">INOVA HOUSE</h1>
    <div class="container">
      <div class="card" v-for="casa in casas" :key="casa.id">
        <img class="card--avatar" :src="casa.image" :alt="casa.title" />
        <h1 class="card--title">{{ casa.title }}</h1>
        <!-- <p>{{ casa.description }}</p> -->
        <p>{{ formatPrice(casa.price) }}</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
  justify-content: center;
  align-items: center;
  margin: auto;
  padding: 1rem 0;
}
.card {
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-direction: column;
  width: 15rem;
  height: 25rem;
  background: #fff;
  box-shadow:
    0 10px 20px rgba(0, 0, 0, 0.19),
    0 6px 6px rgba(0, 0, 0, 0.23);
  border-radius: 10px;
  margin: auto;
  overflow: hidden;
}
.card--avatar {
  width: 100%;
  height: 17rem;
  object-fit: cover;
  margin-bottom: 0.5rem;
}
.card--title {
  color: #000000;
  font-weight: 700;
  text-transform: capitalize;
  font-size: 1.1rem;
  margin-top: 0.5rem;
}

.title {
  flex-direction: column;
  display: flex;
  align-items: center;
  background-color: #000000;
  color: rgb(255, 136, 0);
}
</style>
