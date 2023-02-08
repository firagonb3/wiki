<script setup>
import { ref, onMounted, getCurrentInstance  } from 'vue';
import { useRoute } from 'vue-router';



const api = ref(null)
const digimonId = useRoute().params.id

async function getDigimonById(digimonId) {
    const res = await fetch(`https://digimon-api.com/api/v1/digimon/${digimonId}`);
    let resJson = await res.json()
    api.value = resJson
}

onMounted(() => { getDigimonById(digimonId)});

</script>

<template>
    <div v-if="api">
        <div class="img">
            <h1>{{ api.name }}</h1>
            <img :src="api.images[0].href">
        </div>
        <div class="contenedor">
            <div>
                <h3>prior Evolutions</h3>
                <span v-for="evolucion in api.priorEvolutions">
                    <RouterLink :to="{ name: 'detail', params: { id: evolucion.id }}" >{{ evolucion.digimon }}</RouterLink>,  
                </span>
            </div>
            <div>
                <h3>next Evolutions</h3>
                <span v-for="evolucion in api.nextEvolutions">
                    <RouterLink :to="{ name: 'detail', params: { id: evolucion.id } }">{{ evolucion.digimon }}</RouterLink>,  
                </span>
            </div>
        </div>
    </div>
</template>

<style scoped>
.img {
    margin-top: 5vh;
    display: flex;
    justify-content: space-around;
    flex-direction: column;
    text-align: center;
    align-items: center;
}
.img img{
    max-width: 50vh;
    max-width: 60vw;
}
.contenedor {
    position: absolute;
    width: 100vw;
    right: 0;
    display: flex;
    justify-content: space-around;
}

.contenedor div {
    position: relative;
    max-width: 45vw;
}

</style>