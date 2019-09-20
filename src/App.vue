<template>
  <div>

    <ul>
      <li v-for="foto of fotos" :key="foto.titulo">
        <img :src="foto.url" :alt="foto.titulo">
      </li>
    </ul>
    
  </div>
</template>

<script>
export default {
  data(){
    return {
      titulo: 'Alurapic',
      fotos: [
        
      ]
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

</style>
