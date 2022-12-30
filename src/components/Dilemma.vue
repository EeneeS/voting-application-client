<template>
    <div class="bg-slate-600 inline-block p-16 rounded-lg text-white w-2/3 xl:w-1/4">
        <h2 class="text-4xl">Dilemma:</h2>
        <h3 class="mb-4 mt-2 text-3xl">{{ dilemma.dilemma }}</h3>
        <div class="flex flex-col md:flex-row gap-6 justify-center">
            <Choice v-if="choice1" :choice="choice1" :color="true"></Choice>
            <Choice v-if="choice2" :choice="choice2" :color="false"></Choice>
        </div>
    </div>
</template>

<script>
import Choice from "../components/Choice.vue";
export default {
    name: "Dilemma",
    components: {
        Choice,
    },
    data() {
        return {
            dilemmas: [],
            dilemma: {},
            waitingForNetwork: true,
        }
    },
    methods: {
        async fetchDilemmas() {
            const res = await fetch("http://localhost:5001/quotes");
            const data = await res.json();
            return data;
        },
        async fetchDilemmaById(id) {
            this.waitingForNetwork = true;
            const res = await fetch(`http://localhost:5001/quotes/${id}`);
            const data = await res.json();
            this.waitingForNetwork = false;
            return data[0];
        },
        getRandomNumber() {
            return Math.floor(Math.random() * this.dilemmas.length + 1);
        }
    },
    async created() {
        this.dilemmas = await this.fetchDilemmas();
        this.dilemma = await this.fetchDilemmaById(this.getRandomNumber());
    },
    computed: {
        choice1() {
            return this.dilemma.choice1;
        },
        choice2() {
            return this.dilemma.choice2;
        }
    }
}
</script>