<template>
  <div class="container">

    <div class="card">
    <div class="card-content">
      <h1> Campos calculados </h1>
      <p> {{ nomeCompleto }} </p>
      <input type="text" v-model="nome"/>
    </div>
    </div>

    <br/>
    <input type="text" 
        class="input"
        v-model="filtro"
        placeholder="Digite um nome para pesquisar"
    />
    <table class="table is-bordered">
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
    <input type="number" v-model.number="minima" placeholder="Mínima"/>
    <fahrenheit-temperature :minima="minima" 
        @selecionar="retornarTemperatura" 
        :maxima="300">
    </fahrenheit-temperature>

    <h2> Componente </h2>

     <multiselect v-model="carroSelecionado" 
            :multiple="true"
            track-by="id"
            :options="carros" label="nome"></multiselect>

    {{carroSelecionado}}

    <button @click="ativo=true">Abrir modal</button> 
    <modal 
        :ativo="ativo" 
        :titulo="tituloDaJanela"
        @close="ativo=false" 
        @salvar="salvar">

      <span slot="conteudo">
        <div>
          <input type="text" placeholder="Nome"/>
        </div>
      </span> 

        
    </modal>

  </div>
</template>

<script>
import FahrenheitTemperature from "@/components/FahrenheitTemperature"
import Multiselect from 'vue-multiselect'
import Modal from '@/components/Modal'
export default {
  components: {
    FahrenheitTemperature, Multiselect, Modal
  },
  data() {
    return {
      tituloDaJanela: 'Cliente',
      ativo: false,
      nome : 'Fabiano',
      sobrenome: 'Oss',
      filtro: '',
      minima: 0,
      carroSelecionado: null,
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
  },
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
  },
  methods: {
    retornarTemperatura(t) {
      alert("Celsius: " + t.celsius  +
            "\nFahrenheit: " + t.fahrenheit
            )
    },
    salvar() {
      this.ativo = false
    }
  }
}
</script>

<style src="vue-multiselect/dist/vue-multiselect.min.css"></style>
<style>
</style>
