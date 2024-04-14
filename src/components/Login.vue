<template>
  <div class="home">     

      <div class="buttons-container">
        <button class="button" @click="irABuscarPokemon">Buscar Pokémon</button>
        <button class="button" @click="irAPlayPokemon">Adivinar Pokémon</button>
      </div>
      <div class="containerImagen">
        <p>{{ nombrePokemon }}</p>
        <img class="imagenFondo1" :src="imagenActual">
     
      </div>

    

  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useRouter } from 'vue-router';
import axios from 'axios';

const router = useRouter();
const imagenActual = ref('');
const nombrePokemon = ref('');

const irABuscarPokemon = () => {
  router.push('/BuscarPokemon');
}

const irAPlayPokemon = () => {
  router.push('/AdivinaPokemon');
}

onMounted(async () => {
  await cambiarImagen(); // Cargar la primera imagen al iniciar el componente
  setInterval(cambiarImagen, 3000); // Cambiar la imagen cada 3 segundos
});

async function cambiarImagen() {
  try {
    const idAleatorio = Math.floor(Math.random() * 1024) + 1;
    const resultado = await axios.get(`https://pokeapi.co/api/v2/pokemon/${idAleatorio}`);
    const pokemonData = resultado.data;
    imagenActual.value = pokemonData.sprites.other['official-artwork'].front_default;
    nombrePokemon.value = pokemonData.name;
  } catch (error) {
    console.log(error);
  }
}
</script>


<style>

body {
  background: rgb(252, 237, 28);
  background: linear-gradient(-45deg, rgba(252, 237, 28, 1) 0%, rgba(6, 188, 228, 1) 100%);
}

.home {
  display: grid;
  grid-template-columns: 40% 60%;
    height: 100vh;
}


.containerImagen{
  text-align: center;
}
.imagenFondo1 {
   margin-bottom: 5%;
  transform: scale(1);
  text-align: center;
  
}
.containerImagen p{
font-size: 400%;
padding-top: 5%;
}

.buttons-container {   
    align-items: center;
    margin-left: 20%;
    padding-top: 20%;
}

.button {
  font-size: 280%;
  padding: 10px 20px;
  margin: 6%;
  background-color: #fced1c;
  border: none;
  border-radius: 10px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.button:hover {

  background-color: #888229;
  color: #ffffff;

}

@media (max-width: 1000px) {
  .imagenFondo {
    transform: scale(.7);
  }

  .button {
    font-size: 200%;
  }
  .containerImagen p{
font-size: 300%;

}
}
</style>
