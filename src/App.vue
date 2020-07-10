<template>
  <div class="corpo">
    <h1 class="centralizado">{{titulo}}</h1>

    <input type="search" class="filtro" @input="filtro = $event.target.value" placeholder="filtre por parte do título"/>

    <ul class="lista-fotos">
      <li class="lista-fotos-item" v-for="foto of fotosComFiltro"  v-bind:key="foto.titulo">
        <Painel :titulo="foto.titulo">
          <ImageResponsiva :url="foto.url" :titulo="foto.titulo" />
        </Painel>
      </li>
    </ul>
  </div>
</template>

<script>

import Painel from './components/shared/painel/Painel.vue';
import ImageResponsiva from './components/shared/imagem-responsiva/ImagemResponsiva.vue';

export default {
  components: {
    Painel,
    ImageResponsiva
  },
  name: 'App',
  data() {
    return {
      titulo: 'AluraPIC',
      fotos: [],
      filtro: ''
    }
  },

  computed: {

    fotosComFiltro() {

      if(this.filtro) {
        let exp = new RegExp(this.filtro.trim(), 'i');
        return this.fotos.filter(foto => exp.test(foto.titulo));
      } else {
        return this.fotos;
      }
    }
  },

  created() {
    this.$http.get('http://localhost:3000/v1/fotos')
      .then(res => res.json())
      .then(fotos => this.fotos = fotos, err => console.log(err));
  }

}
</script>

<style>
  .corpo {
    font-family: Helvetica, sans-serif;
    width: 96%;
    margin: 0 auto;
  }

  .centralizado {

    text-align: center;
  }

  .lista-fotos {
    list-style: none;
  }

  .lista-fotos .lista-fotos-item {

    display: inline-block;
  }

  .filtro {

    display: block;
    width: 100%;
  }
</style>
