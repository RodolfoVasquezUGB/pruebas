<template>
     <div id="contenido">
    <lenguaje-com/>
    <br/>
    <hr/>
    <lenguaje-crear @reloadpage="reloadpage" />
  </div>
</template>


<script>
import LenguajeCrear from '../components/LenguajeCrear.vue';
import LenguajeCom from '../components/LenguajeList.vue'
export default {
    name: 'LenguajeView',
    components: {
        LenguajeCom,
        LenguajeCrear
    },
    methods: {
        reloadpage() {
        window.location.reload();
        },
    },
}
</script>

<style>

</style>