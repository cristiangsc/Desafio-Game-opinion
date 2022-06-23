<template>
    <div class="text-center">
        <img class="w-50 my-5" src="../assets/notfound.png" alt="">
        <h1>La página que buscas no existe </h1>
        <router-link :to="{name: 'home'}">Volver al inicio</router-link>
        <br>
    </div>
</template>