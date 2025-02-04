<template>
  <h1>Food</h1>
  <ul>
    <li v-for="country in countries" :key="country.id">{{ country.name }}</li>
  </ul>
  <br>
  <personal-profile/> <br>
  <food-item/> 
  <food-item2/> 
  <food-item/> 

  <!-- Add comment section -->
  <div class="comments-section">
    <comment-form @comment-submitted="addComment"/>
    <comment-list :comments="comments"/>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { supabase } from './lib/supabaseClient'
import CommentForm from '@/components/CommentForm.vue'
import CommentList from '@/components/CommentList.vue'

const countries = ref([])
const comments = ref([])

async function getCountries() {
  const { data } = await supabase.from('countries').select()
  countries.value = data
}

function addComment(newComment) {
  comments.value.push(newComment)
}

onMounted(() => {
  getCountries()
})
</script>

<style>
.comments-section {
  margin-top: 40px;
  padding: 20px;
}
</style>