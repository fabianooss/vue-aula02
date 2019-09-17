<template>
  <div id="app">
    <h1> Campos calculados </h1>
    <p> {{ nomeCompleto }} </p>
    <input type="text" v-model="nome"/>

    <br/>
    <input type="text" 
        v-model="filtro"
        placeholder="Digite um nome para pesquisar"
    />
    <table>
      <tr>
        <th>Id</th>
        <th>Nome</th>
      </tr>
      <tr v-for="c in carrosFiltrados" :key="c.id">
        <td>{{c.id}}</td>
        <td>{{c.nome}}</td>
      </tr>
    </table>

    <h1>Observadores</h1>

  </div>
</template>

<script>

export default {
  data() {
    return {
      nome : 'Fabiano',
      sobrenome: 'Oss',
      filtro: '',
      carros: [
        { nome: 'Lamborguini', id: 1},
        { nome: 'Fusca', id: 2},
        { nome: 'R-34', id: 3},
        { nome: 'Chevete', id: 4},
        { nome: 'Monza', id: 5},
      ]
    }
  },
  beforeMount() {
    /* eslint-disable */
    console.log('antes de montar os componentes')
  },
  mounted() {
    /* eslint-disable */
    console.log('mountou os componentes')
  },
  updated() {
    /* eslint-disable */
    console.log('atualizou os componentes')
ç  },
  watch: {
    nome: function (val) {
      /* eslint-disable */
      console.log('Modificou o nome ' + val)
    },
    carrosFiltrados: function(val) {
      /* eslint-disable */
      console.log('Modificou o array ' + val)      
    }
  },
  computed: {
    nomeCompleto: function() {
      return this.nome + " " + this.sobrenome
    },
    carrosFiltrados: function() {
      if (this.filtro == '') {
        return this.carros
      }
      return this.carros.filter(c => {
        return c.nome.startsWith(this.filtro)
      })
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
