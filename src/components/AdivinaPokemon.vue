<template>
  <div>
    <div class="nameId">
      <button @click="buscarPokemonAleatorio()">Mostrar Pokémon Aleatorio</button>
    </div>
    <div class="container-1">
      <div class="container-2">
        <div class="nameId">
          <label>
            Nombre del Pokémon<br>
            <input type="text" v-model="nombrePokemon" :disabled="adivinado">
          </label>
        </div>
        <div class="contador" v-if="!adivinado">{{ contador }}</div>
      </div>
      <div class="container-2">
        <div class="nameImg">
          <section v-if="pokemonData" class="card">
            <h2 class="namePokemon" v-if="nombrePokemon === pokemonData.name">{{ pokemonData.name }}</h2>
            <p>Numero: {{ pokemonData.id }}</p>
            <p>Peso: {{ pokemonData.weight }}</p>
            <div class="imagen">
              <img :src="pokemonData.sprites?.front_shiny" :alt="pokemonData.name"
                   :class="{ 'pokemonImage': 1, 'coloredImage': (nombrePokemon === pokemonData.name) }">
            </div>
          </section>
        </div>
      </div>
      <h4 id="alerta" v-if="error != ''">{{ error }}</h4>
    </div>
    <ul class="type" v-if="pokemonData && nombrePokemon === pokemonData.name">
      <h3>Tipo:</h3>
      <li v-for="(type, index) in pokemonData.types" :key="index" :class="type.type.name">
        <span>{{ type.type.name }}</span>
      </li>
    </ul>
    <ul class="stat" v-if="pokemonData && nombrePokemon === pokemonData.name">
      <h3>Estadisticas:</h3>
      <li v-for="(stat, index) in pokemonData.stats" :key="index">
        <span>{{ stat.stat.name }}:</span>
        <progress :value="stat.base_stat" max="255"></progress>
        <span>{{ stat.base_stat }}</span>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from "vue"
import axios from "axios"

let pokemonData = ref(null)
let nombrePokemon = ref("")
let error = ref("")
let contador = ref(0)
let adivinado = ref(false)

async function buscarPokemonAleatorio() {
  try {
    const idAleatorio = Math.floor(Math.random() * 1024) + 1;
    const resultado = await axios.get(`https://pokeapi.co/api/v2/pokemon/${idAleatorio}`)
    pokemonData.value = resultado.data
    console.log(resultado.data)
    nombrePokemon.value = ""
    contador.value = 30
    adivinado.value = false 


    // Verificar si el nombre se ha adivinado
    if (nombrePokemon.value === pokemonData.value.name) {
      contador.value = 30
      adivinado.value = true
    }

    // Iniciar el contador
    const interval = setInterval(() => {
      contador.value--;
      if (contador.value === 0) {
        clearInterval(interval);
        error.value = "¡Perdiste!";
        setTimeout(() => {
          error.value = "";
        }, 3000);
      }
    }, 1000);

  } catch (error) {
    console.log(error)
    error.value = "Se produjo un error al cargar el Pokémon."
  }
}
</script>

<style scoped>
.container-1 {
  display: flex;
  height: 100%;
}

.container-2 {
  flex: 1;
  text-align: center;
}

.pokemonImage {
  filter: brightness(0%) grayscale(100%);
}

.coloredImage {
  filter: none;
}

.nameId {
  margin-bottom: 2%;
}

.contador {
  font-size: 300%;
  background-color: #fced1c;
  width: 20%;
  border-radius: 10px 0;
  margin-left: 40%;
}
</style>
