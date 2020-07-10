<template>
  <div>
    <h1 class="painel-titulo" @dbclick="visivel = !visivel">{{titulo}}</h1>
    <transition name="painel-fade">
      <div class="painel-conteudo" v-show="visivel">
        <slot></slot>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  props: ['titulo'],

  data() {
    return {
      visivel: true
    }
  }
}
</script>

<style>

</style>