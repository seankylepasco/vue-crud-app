<template>

    <button :style='{background: color}' @click='onClick()'>{{ name }}</button>
</template>


<script>
export default {
    name: 'Button',
    props: {
        name: String,
        color: String,
    },
    methods: {
        onClick() {
            console.log('clicked!')
        }
    }
}
</script>
