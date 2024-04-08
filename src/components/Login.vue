<template>
  <div class="home">
    <img class="imagenFondo" src="../imagenes/poke1.png">  
    <div class="Fondo">  
       
      <div class="buttons-container">
        <button class="button" @click="irABuscarPokemon">Buscar Pokémon</button>
        <button class="button" @click="irAPlayPokemon">Adivinar Pokémon</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { useRouter } from 'vue-router';

const router = useRouter();

const irABuscarPokemon = () => {
  router.push('/BuscarPokemon');
}

const irAPlayPokemon = () => {
  router.push('/AdivinaPokemon');
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

.Fondo {
  border: solid 2px black;
 border-radius: 50%;
 width: 100px;
}
.imagenFondo{
  margin-top: 5%;
  margin-bottom: 5%;
  transform: scale(0.28);
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
  font-size: 24px;
  padding: 10px 20px;
  margin: 10px;
  background-color: #f17d11;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.button:hover {
  
  background-color: #c4670b;
}
</style>
