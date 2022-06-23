<template>
    <div>
        <header class="text-center my-5">
            <h1>Lista de Opiniones</h1>
        </header>
        <new-comments/>

    </div>
</template>
<script>
import newComments from '@/components/NewComments.vue'
    export default {
        components:{
            newComments
        }
    }
</script>
<style scoped>
h1{
  text-align: center;
}
</style>