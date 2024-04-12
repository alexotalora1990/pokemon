<template>
  <div class="home">
    <img class="imagenFondo" :src="imagenActual">  
    <div class="Fondo">  
       
      <div class="buttons-container">
        <button class="button" @click="irABuscarPokemon">Buscar Pokémon</button>
        <button class="button" @click="irAPlayPokemon">Adivinar Pokémon</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useRouter } from 'vue-router';
import axios from 'axios';

const router = useRouter();
const imagenActual = ref('');

const irABuscarPokemon = () => {
  router.push('/BuscarPokemon');
}

const irAPlayPokemon = () => {
  router.push('/AdivinaPokemon');
}

onMounted(() => {
  setInterval(cambiarImagen, 3000); // Cambia la imagen cada 3 segundos
});

async function cambiarImagen() {
  try {
    const idAleatorio = Math.floor(Math.random() * 1024) + 1;
    const resultado = await axios.get(`https://pokeapi.co/api/v2/pokemon/${idAleatorio}`);
    const pokemonData = resultado.data;
    imagenActual.value = pokemonData.sprites.other['official-artwork'].front_default;
  } catch (error) {
    console.log(error);
  }
}
</script>

<style>
body {
  background: rgb(252,237,28);
background: linear-gradient(-45deg, rgba(252,237,28,1) 0%, rgba(6,188,228,1) 100%);
}
.home {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}


.imagenFondo{
  margin-top: 5%;
  margin-bottom: 5%;
  transform: scale(1);
  margin-left: 50%;
}



.buttons-container {
  position: absolute;
  top: 50%;
  left: 30%;
  transform: translate(-50%, -50%);
  display: flex;
  flex-direction: column;
  align-items: center;
}

.button {
  font-size: 300%;
  padding: 10px 20px;
  margin: 10px;
  background-color: #fced1c;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.button:hover {
  
 
  background-color: #888229;
  color: #ffffff;

}

@media (max-width: 1000px){
  .imagenFondo {
  transform: scale(.7);  
  }
  .button {
  font-size: 200%;
  }
}

</style>
