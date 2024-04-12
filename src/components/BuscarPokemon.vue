<template>
  <div>

    <div class="nameId">
      <h4 id="alerta" v-if="error != ''">{{ error }}</h4>
      <label>
        <p class="parrafo">Nombre de pokemon o id:</p>
        <input type="text" v-model="idPokemon">
        <button @click="validar()">Buscar Pokemon</button>
      </label>
    </div>
    <div class="container">
      <div class="container1">
        <section v-if="pokemonData" class="card">
          <h2 class="namePokemon">{{ pokemonData.name }}</h2>
          <p>Numero: {{ pokemonData.id }}</p>
          <p>Peso: {{ pokemonData.weight }}</p>

          <ul class="type" v-if="pokemonData">
            <h3>Tipo:</h3>
            <li v-for="(type, index) in pokemonData.types" :key="index" :class="type.type.name">
              <span>{{ type.type.name }}</span>
            </li>
          </ul>
        </section>
      </div>
      <div class="imagen">
        <img v-if="pokemonData && pokemonData.sprites"
          :src="pokemonData.sprites.other?.['official-artwork']?.front_default" :alt="pokemonData.name">
      </div>
    </div>


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
    idPokemon.value=""
  }
}

async function traer() {
  try {
    const resultado = await axios.get(`https://pokeapi.co/api/v2/pokemon/${idPokemon.value}`)
    pokemonData.value = resultado.data
    console.log(resultado.data)
    console.log(pokemonData.value.name)
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
  background-color: #fced1c;
   color: black;
  cursor: pointer;
 
}

.container {
  display: flex;
  height: 100%;
  padding-top: 5%;
}

.container1 {
  display: 1;
  text-align: center;
  padding-left: 10%;

}

.container1 section p {
  font-size: 200%;
  text-align: left;
  margin-top: 5%;

}

/* Estilos para la tarjeta de Pokemon */
.card {
width: 140%;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
  padding: 15%;
  margin-top: 3%;
}



.namePokemon {
  color: #000000;
  /* Negro */
  text-align: center;
  font-size: 500%;
}

.imagen {
  text-align: center;
  height: auto;
  display: block;
  margin: 0 auto;
  transform: scale(1);
  margin-bottom: 3%;
  padding-left: 10%;
  

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

.li span,
.stat li span {
  margin-right: 10px;
  font-size: 200%;
  padding: 5px 10px;
  border-radius: 4px;
  background-color: #fced1c;

}

.type{
  font-size: 200%;
text-align: center;
  border-radius: 4px;
  background-color: #fced1c;
}

progress {
  width: 100%;
  height: 30px;
  margin: 1% 3%;
  background-color: #fced1c;
  border-radius: 10px;

}

.parrafo {
  font-size: 180%;
}

button:hover {
  background-color: #888229;
  color: #ffffff;
}

@media (max-width: 1000px){
  .imagen {
  transform: scale(.8);  
  }
  .h3{
  font-size: 100%;
}
.namePokemon {
  font-size: 350%;
}
}
</style>