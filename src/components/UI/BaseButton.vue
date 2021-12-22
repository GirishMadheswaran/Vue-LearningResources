<template>
    <button :class="mode">
        <slot></slot>
    </button>
</template>

<script>
export default {
    props:['mode']
}
</script>

<style scoped>
    button{
        padding: 0.75rem 1.5rem;
        background-color: brown;
        border: 1px solid black;
        color: white;
        cursor: pointer;
    }
    button:hover,
    button:active{
        background-color: chocolate;
        border-color: cornsilk;
    }
    .flat{
        background-color: transparent;
        color: violet;
        border: none;
    }
    .flat:hover,
    .flat:active{
        background-color: #edd2ff;
    }
</style>