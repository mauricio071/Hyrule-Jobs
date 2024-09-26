<template>
    <div class="job-list">
        <p class="filter">Filtrado por: {{ filtro }}</p>
        <transition-group name="list" tag="ul">
            <li v-for="job in jobsOrdenado" :key="job.id">
                <h2>{{ job.titulo }} em {{ job.local }}</h2>
                <div class="salary">
                    <img src="../assets/rupee.svg" alt="rupee">
                    <p>{{ job.salario }} rupees</p>
                </div>
                <div class="description">
                    <p>{{ job.descricao }}</p>
                </div>
            </li>
        </transition-group>
    </div>
</template>

<script lang="ts">
import { defineComponent, PropType, ref, computed } from 'vue';
import Job from '../types/Job';
import Ordem from '../types/OrderTerm';

export default defineComponent({
    name: 'JobList',
    props: {
        jobs: {
            required: true,
            type: Array as PropType<Job[]>
        },
        filtro: {
            required: true,
            type: String as PropType<Ordem>
        }
    },
    setup(props) {
        const jobsOrdenado = computed(() => {
            return [...props.jobs].sort((a: Job, b: Job) => {
                return a[props.filtro] > b[props.filtro] ? 1 : -1
            })
        })

        return { jobsOrdenado }
    }
});
</script>

<style scoped>
.filter {
    font-size: 20px;
    font-weight: bold;
}

.job-list {
    max-width: 960px;
    margin: 40px auto;
}

.job-list ul {
    padding: 0;
}

.job-list li {
    list-style-type: none;
    background: white;
    padding: 16px;
    margin: 16px 0;
    border-radius: 4px;
}

.job-list h2 {
    margin: 0 0 10px;
    text-transform: capitalize;
}

.salary {
    display: flex;
}

.salary img {
    width: 30px;
}

.salary p {
    color: #17bf66;
    font-weight: bold;
    margin: 10px 4px;
}

.list-move {
    transition: all 1s;
}
</style>