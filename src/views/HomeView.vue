<script setup>
import { ref, watch } from 'vue'
import d from '../data/data.json'

const digimon = ref(d)
const search = ref('')
const api = ref([])

watch(search, () => {
  if (search.value === '') {
    api.value = "";
  } else {
    api.value = digimon.value.filter(digimon => digimon.name.toLowerCase().includes(search.value.toLowerCase()))
  }

})
</script>

<template>
  <div class="input">
    <label>Digimon: </label>
    <div>
      <input v-model="search" type="text" placeholder="Search">
      <ul>
        <li v-for="item in api">
          <RouterLink :to="{ name: 'detail', params: { id: item.id } }">{{ item.name }}</RouterLink>
        </li>
      </ul>
    </div>
  </div>
</template>

<style scoped>
.input {
  margin-top: 5vh;
  margin-left: 5vw;
}

input {
  width: 25em;
  height: 2em;
  border-radius: 5px;
  left: 1em;
  padding-left: 1em;
}

input::before {
  content: "ddd";
  color: red;
}
.input div {
  position: absolute;
}

.input div ul {
  position: absolute;
  list-style-type: none;
  background-color: white;
  width: 100%;
  border-end-end-radius: 5px;
  border-end-start-radius: 5px;
  max-height: 50vh;
  overflow-y: scroll;
  overflow-x: hidden;
}

.input div li {
  position: relative;
  padding-left: .5em;
  padding-top: .2em;
}

.input div li:last-child {
  padding-bottom: .5em;
}
</style>