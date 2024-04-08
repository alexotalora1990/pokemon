<template>
  <div>
    
        <div class="nameId">
          <h4 id="alerta" v-if="error != ''">{{ error }}</h4>
      <label>
        Nombre de pokemon o id:
        <input type="text" v-model="idPokemon">
        <button @click="validar()">Buscar Pokemon</button>
      </label>
      
    </div>
    <div class="nameImg">
      <section v-if="pokemonData" class="card">
        <h2 class="namePokemon">{{ pokemonData.name }}</h2>
        <p>Numero: {{ pokemonData.id }}</p>
        <p>Peso: {{ pokemonData.weight }}</p>
<div class="imagen">
  <img :src="pokemonData.sprites?.front_shiny" :alt="pokemonData.name">
</div>
        
      </section>
    </div>
    <ul class="type" v-if="pokemonData">
      <h3>Tipo:</h3>
      <li v-for="(type, index) in pokemonData.types" :key="index" :class="type.type.name">
        <span>{{ type.type.name }}</span>
      </li>
    </ul>
    <ul class="stat" v-if="pokemonData">
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
let idPokemon = ref("")
let error = ref("")
function validar() {
  if (idPokemon.value === "") {
    error.value = "Digite un nombre o un id"
    setTimeout(() => {
      error.value = ""
    }, 3000)
  }

  else {
    traer()
  }
}

async function traer() {
  try {
    const resultado = await axios.get(`https://pokeapi.co/api/v2/pokemon/${idPokemon.value}`)
    pokemonData.value = resultado.data
    console.log(resultado.data)
    console.log(pokemonData.value.stats)
  } catch (error) {
    console.log(error)
  }
}

</script>

<style>
* {
  margin: 0;
  font-family: Arial, "Helvetica Neue", Helvetica, sans-serif;
}



#alerta {
  text-align: center;
  width: 36%;
  box-shadow: 7px 7px 14px #807c7c,
    -7px -7px 14px #807c7c;
  z-index: 1200;
  margin-left: 28%;

}

h4 {
  width: 100%;
  height: 100px;
  padding: 2%;
  padding-top: 2%;
  text-align: center;
  border-radius: 10px;
  background-color: red;
  color: #ffffff;
  position: fixed;
}

/* Estilos para el contenedor principal */
.nameId {
  padding-top: 5%;
  text-align: center;
  font-size: 120%;

}

/* Estilos para el formulario de búsqueda */
input[type="text"] {
  padding: 8px;
  border-radius: 4px;
  border: 1px solid #ccc;
  margin-right: 1%;
}

button {
  padding: 8px 16px;
  border: none;
  border-radius: 4px;
  background-color:  #eca013 ;
  /* Verde */
  color: black;
  cursor: pointer;
  font-size: 120%;

}

/* Estilos para la tarjeta de Pokemon */
.card {
  
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  padding: 20px;
  margin-top: 20px;
}

.card p {
  font-size: 120%;
  text-align: right;
  margin-right: 5%;
}

.namePokemon {
  color: #333;
  /* Negro */
  text-align: center;
  font-size: 200%;
}

.imagen {
  max-width: 100%;
  text-align: center;
  height: auto;
  display: block;
  margin: 0 auto;
  transform: scale(2);
  margin-bottom: 3%;
  
}

/* Estilos para las listas de tipo y estadísticas */
.type,
.stat {
  margin-top: 2%;
  width: 80%;
  margin-left: 10%;
}

.type h3,
.stat h3 {
  margin-bottom: 2%;
}

.type li,
.stat li {
  list-style: none;
  margin-bottom: 1%;
}

.type li span,
.stat li span {
  margin-right: 10px;
  padding: 5px 10px;
  border-radius: 4px;
  background-color: #f17d11;
  color: white;
}

progress {
  width: 100%;
  height: 30px;
  margin: 1% 3%;
  background-color: #4CAF50; 
  border-radius: 10px; 

}
</style>