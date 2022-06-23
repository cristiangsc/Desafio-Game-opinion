<template>
    <div>
        <header>
            <h1 class="my-4">Lista de Juegos Disponibles</h1>
        </header>
        <cards/>
    </div>
</template>

<script>
    import Cards from '@/components/Cards.vue'
    export default {
        components: {
            Cards: Cards
        },
    }
</script>

<style scoped>
h1{
  text-align: center;
}
</style>