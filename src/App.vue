<template>
  <div class="app">
    <header>
      <div class="title">
        <img src="./assets/heart.svg" alt="logo">
        <h1>Hyrule Jobs</h1>
      </div>
      <div class="order">
        <button @click="filtrar(Ordem.titulo)">Ordenar por título</button>
        <button @click="filtrar(Ordem.local)">Order por local</button>
        <button @click="filtrar(Ordem.salario)">Order por salario</button>
      </div>
    </header>
    <job-list :jobs="jobs" :filtro="filtro" />
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import JobList from './components/JobList.vue';
import Job from './types/Job';
import Ordem from './types/OrderTerm';

export default defineComponent({
  name: 'App',
  components: { JobList },
  setup() {
    const jobs = ref<Job[]>([
      { id: 1, titulo: 'fazendeiro', local: 'lon lon ranch', salario: 30000, descricao: 'No coração do campo, o fazendeiro trabalha duro cultivando e cuidando do gado em Lon Lon Ranch. Conhecido por sua habilidade em criar vacas e produzir leite de alta qualidade, ele é a espinha dorsal da economia rural. O trabalho exige dedicação, conhecimento agrícola e uma conexão especial com a natureza.' },
      { id: 2, titulo: 'guerreiro', local: 'death mountain', salario: 40000, descricao: 'Como guerreiro de Death Mountain, este profissional é responsável por proteger as fronteiras montanhosas e enfrentar criaturas ferozes que habitam a região. O treinamento rigoroso e a bravura são essenciais para sobreviver nos perigosos terrenos vulcânicos. Um trabalho para quem possui força física e coragem.' },
      { id: 3, titulo: 'caçador', local: 'the lost woods', salario: 35000, descricao: 'Explorando as misteriosas e labirínticas florestas de The Lost Woods, o caçador é um mestre em rastreamento e sobrevivência. Ele caça criaturas raras e recolhe recursos preciosos, ajudando a manter o equilíbrio da natureza. Apenas os mais astutos conseguem sair ilesos dessas florestas mágicas.' },
      { id: 4, titulo: 'mago', local: 'lake hylia', salario: 21000, descricao: 'O mago de Lake Hylia é conhecido por sua sabedoria e domínio das artes mágicas. Ele vive isolado nas margens do lago, onde estuda antigos feitiços e guarda segredos do mundo mágico. Suas habilidades são requisitadas em momentos de crise, e sua conexão com as águas místicas é incomparável.' },
      { id: 5, titulo: 'guarda', local: 'gerudo valley', salario: 32000, descricao: 'O guarda de Gerudo Valley é responsável pela segurança e manutenção da ordem nesta região desértica. Protegendo as passagens e controlando o fluxo de viajantes, ele precisa estar sempre alerta. Gerudo Valley é conhecida por sua cultura guerreira, e esse cargo é destinado a quem busca respeito e autoridade.' }
    ])

    const filtro = ref<Ordem>(Ordem.titulo)

    function filtrar(ordem: Ordem) {
      filtro.value = ordem;
    }

    return { jobs, filtro, filtrar, Ordem }
  },
});
</script>

<style>
header {
  text-align: center;
}

header .order {
  margin-top: 20px;
}

button {
  margin: 0 10px;
  color: #1195c9;
  border: 3px solid #1195c9;
  background: #d5f0ff;
  padding: 8px 16px;
  border-radius: 4px;
  cursor: pointer;
  font-weight: bold;
}

header .title {
  display: flex;
  justify-content: center;
}

header img {
  width: 60px;
  margin-right: 20px;
}

header h1 {
  font-size: 3em;
}
</style>
