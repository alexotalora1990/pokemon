<template>
  <q-layout view="hHh lpR fFf">

    <q-header elevated class="bg-primary text-black" height-hint="98">
      <q-toolbar>
        <!-- <q-btn dense flat round icon="menu" @click="toggleLeftDrawer" /> -->

        <q-toolbar-title>
          <q-avatar>
            <img src="./imagenes/pokebola.png">
          </q-avatar>
          POKEMON
        </q-toolbar-title>
      </q-toolbar>

      <q-tabs align="left">
        <q-route-tab to="/" label="Inicio" />
        <q-route-tab to="/BuscarPokemon" label="Buscar-Pokemon" />
        <q-route-tab to="/AdivinaPokemon" label="Adivinar-Pokemon" />
      </q-tabs>
    </q-header>

    <!-- <q-drawer v-model="leftDrawerOpen" side="left" behavior="mobile" bordered>
     <router-link to="/">Inicio</router-link>" <br>
     <router-link to="/BuscarPokemon">BuscarPokemon</router-link>"<br>
     <router-link to="/AdivinaPokemon">AdivinaPokemon</router-link>"
    </q-drawer> -->

    <q-page-container>
      <router-view> </router-view >
    </q-page-container>

    <q-footer elevated class="bg-grey-8 text-white">
      <q-toolbar>
        <q-toolbar-title>
          <q-avatar>
           
          </q-avatar>
          <div>Derechos reservados</div>
        </q-toolbar-title>
      </q-toolbar>
    </q-footer>

  </q-layout>
</template>

<script>
import { ref } from 'vue'

export default {
  setup () {
    const leftDrawerOpen = ref(false)

    return {
      leftDrawerOpen,
      toggleLeftDrawer () {
        leftDrawerOpen.value = !leftDrawerOpen.value
      }
    }
  }
}
</script>
<style scoped>
footer{
  text-align: center;
}

</style>
