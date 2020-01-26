<template>
    <div id="app">
        <Calculator/>
    </div>
</template>

<script>
    import Calculator from './components/Calculator'

    export default {
        name: 'App',
        components: {
            Calculator
        }
    }
</script>

<style>
    body {
        overflow-x: hidden;
    }
    #app {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        margin-top: 60px;
    }
</style>
