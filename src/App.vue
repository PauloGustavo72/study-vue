<!-- alurapic/src/App.vue -->
<template>
  <div class="corpo">

    <h1 class="centralizado">{{ titulo }}</h1>

    
    <input class="filtro" v-on:input="filtro = $event.target.value" placeholder="filtre pelo título da foto">

    {{filtro}}
    <ul class="lista-fotos">

      <li class="lista-fotos-item" v-for="foto in fotosComFiltro" :key="foto.titulo">

        <meu-painel :titulo="foto.titulo">
            <imagem-responsiva :url="foto.url" :alt="foto.titulo"/>
        </meu-painel>

      </li>
    </ul>

  </div>
</template>

<script>

// importando nosso Painel 

import Painel from './components/shared/painel/Painel.vue';
import ImagemResponsiva from './components/shared/imagem-responsiva/ImagemResponsiva.vue';

export default {


  components: {

    'meu-painel': Painel,
    'imagem-responsiva' : ImagemResponsiva
  },

  data(){
    return {
      titulo: 'Alurapic',
      fotos: [],
      filtro : ''
    }
  },

  computed: {
    fotosComFiltro(){
      if(this.filtro){
        let exp = new RegExp(this.filtro.trim(), 'i');
        return this.fotos.filter(foto => exp.test(foto.titulo))
      }else{
        return this.fotos;
      }
    }
  },

  created(){
    this.$http.get('http://localhost:3000/v1/fotos')
      .then(resp => resp.json())
      .then(fotos => this.fotos = fotos, err => console.log(err));
  }

}
</script>

<style>
  
  .titulo {
    text-align: center;
  }

  .corpo {
    font-family: Helvetica, sans-serif;
    margin: 0 auto;
    width: 96%;
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