<template>
    <div class="bg-slate-600 inline-block p-16 rounded-lg text-white w-2/3 xl:w-1/4">
        <h2 class="text-4xl">Dilemma:</h2>
        <h3 class="mb-4 mt-2 text-3xl">{{ dilemma.dilemma }}</h3>
        <div class="flex flex-col md:flex-row gap-6 justify-center">
            <Choice :choice="dilemma.choice1" :color="true"></Choice>
            <Choice :choice="dilemma.choice2" :color="false"></Choice>
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
    props: {
        dilemma: Object,
    },
}
</script>