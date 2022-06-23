<template>
    <div>
        <header class="text-center my-5">
            <h1>Administrar la Lista de Opiniones</h1>
        </header>
        <admin-comments/>
    </div>
</template>
<script>
import adminComments from '@/components/AdminComments.vue'
    export default {
        components:{
            adminComments
        }
    }
</script>
<style>

</style>