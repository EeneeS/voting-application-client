<template>
    <button :class="color ? 'bg-blue-500 hover:bg-blue-600' : 'bg-red-500 hover:bg-red-700'"
            class="p-5 rounded-md text-2xl"
            >
            {{choice}}
    </button>
</template>

<script>
export default {
    name: "Choice",
    props: {
        choice: String,
        color: Boolean
    },
}
</script>