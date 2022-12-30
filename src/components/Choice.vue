<template>
    <button :class="color ? 'bg-blue-500 hover:bg-blue-600' : 'bg-red-500 hover:bg-red-700'"
            class="p-5 rounded-md md:text-2xl md:font-normal font-bold flex flex-col"
            @click="handleClick(choice.choiceId)"
            :disabled="resultsVisible"
            >
            <span v-if="resultsVisible" class="font-bold">
                {{ votePercentage }}%
            </span>
            <span>{{ choice.msg }}</span>
    </button>
</template>

<script>
export default {
    name: "Choice",
    props: {
        choice: Object,
        color: Boolean,
        totalVotes: Number,
        resultsVisible: Boolean,
    },
    data() {
        return {
            clicked: false,
        }
    },
    methods: {
        handleClick(id) {
            this.$emit('handle-vote', id);
        }
    },
    computed: {
        votePercentage() {
            return Math.floor((this.choice.votes / this.totalVotes) * 100);
        },
    },
    emits: ['handle-vote'],
}
</script>