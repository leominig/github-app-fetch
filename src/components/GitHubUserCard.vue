<template>
  <div class="card">
    <div class="image">
      <img :src="user.avatar_url" />
    </div>
    <div class="content">
      <a :href="url + username" class="header">{{ user.name }}</a>
      <div class="meta">
        <span class="date">Joined at {{ user.created_at }}</span>
      </div>
      <div class="description">
        {{ user.location }}
      </div>
    </div>
    <div class="extra content">
      <a>
        <i class="user icon"></i>
        {{ user.followers }} Friends
      </a>
    </div>
  </div>
</template>

<script setup>
import { reactive, ref } from 'vue'
import axios from 'axios'

const props = defineProps(['username'])

const url = ('https://api.github.com/users/')

const user = ref({})


const fetchCardUser = (async () => {
  await axios.get(url + props.username).then(response => {
    user.value = response.data
  })
})


fetchCardUser()

</script>

<style>
</style>