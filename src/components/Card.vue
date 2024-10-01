<script setup>

const props = defineProps({
    bg:{
        type: String,
        default: 'bg-gray-400'
    }
})

</script>

<template>
    <div :class="`${props.bg} p-6 rounded-lg shadow-md`">
        <slot></slot>
    </div>
</template>