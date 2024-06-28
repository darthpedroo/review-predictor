<script setup>
import { ref } from 'vue';
import axios from 'axios';

const data = ref({
  review: '',
});

const response = ref({
  response: '',
});

async function handleSubmit(review) {
  try {
    console.log("REVIEW: ", review);
    const res = await axios.get(`https://porky.pythonanywhere.com/review//${review}`);
    response.value.response = res.data; // Correctly set the response value
  } catch (error) {
    console.error(error);
  }
}
</script>

<template>
  <main>
    <form @submit.prevent="handleSubmit(data.review)">
      <textarea
        id="review"
        v-model="data.review"
        type="text"
        required
      ></textarea>
      <button>SUBMIT</button>
    </form>

    <div class="div">
      <h1>
        TU REVIEW ES UN: {{ response['response'] }}% POSITIVA
    </h1><br>
    <H1>Y UN {{ 1 - response['response'] }}% NEGATIVA</H1> 
    </div>
  </main>
</template>
