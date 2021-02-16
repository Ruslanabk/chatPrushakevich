<template>
    <button class="btn" v-bind:style=" 'background: ' + color ">
        <slot>Текст по умолчанию</slot>
    </button>
</template>

<script>
export default {
    name: 'Button',
    props: ['color', 'text']
}
</script>

<style>
.btn{
    padding: 10px 20px;
    color: #fff;
    background-color: #6c5ce7;
    border-radius: 10px;
    border: 0;
    outline: none;
    cursor: pointer;
}
</style>