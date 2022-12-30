<template>
    <div class="bg-slate-600 inline-block p-16 rounded-lg text-white w-2/3 xl:w-4/6">
        <h2 class="text-4xl">Dilemma:</h2>
        <i v-if="waitingForNetwork" class="fa-solid fa-spinner fa-spin fa-5x text-white text-center mt-8" style="--fa-flip-x: 1; --fa-flip-y: 0;"></i>
        <div v-else>
            <h3 class="mb-4 mt-2 md:text-3xl font-bold">{{ dilemma.dilemma }}</h3>
            <div class="flex flex-col md:flex-row gap-6 justify-center">
                <Choice v-if="choice1" :choice="choice1" :dilemmaId="dilemma.id" @handle-vote="handleVote" :totalVotes="totalVotes" :resultsVisible="resultsVisible" :color="true"></Choice>
                <Choice v-if="choice2" :choice="choice2" :dilemmaId="dilemma.id" @handle-vote="handleVote" :totalVotes="totalVotes" :resultsVisible="resultsVisible" :color="false"></Choice>
            </div>
        </div>
    </div>
    <div v-if="resultsVisible">
        <button 
        @click="nextDilemma"
        class="bg-red-500 mt-16 px-8 py-4 rounded-md text-white font-bold md:mb-0 mb-8"
        >next >
        </button>
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
            waitingForNetwork: false,
            resultsVisible: false,
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
            return data;
        },
        getRandomNumber() {
            return Math.floor(Math.random() * this.dilemmas.length + 1);
        },
        async handleVote(id) {
            this.waitingForNetwork = true;
            const res = await fetch(`http://localhost:5001/quotes/vote/${this.dilemma.id}/${id}`, {
                method: "POST",
                headers: {
                    "Content-Type": "application/js"
                }
            });
            this.dilemma = await res.json();
            this.waitingForNetwork = false;
            this.resultsVisible = true;
        },
        async nextDilemma() {
            this.dilemma = await this.fetchDilemmaById(this.getRandomNumber());
            this.resultsVisible = false;
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
        },
        totalVotes() {
            return this.dilemma.choice1.votes + this.dilemma.choice2.votes;
        }
    }
}
</script>