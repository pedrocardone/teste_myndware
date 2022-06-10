<template>
   <div class="row justify-content-center" v-show="nenhum_signatario">
        <div class="col-auto" style="text-align: center;">
            <img src="src/assets/mailbox.png" width="300px" />
            <h4>Listagem de signatários vazia</h4>
            <p>Adicione os emails para que as pessoas<br/> apareçam aqui nessa lista.</p>         
        </div>
    </div>
</template>



<script>
    export default {
        props:['nenhum_signatario'],

        methods:{      
        }
    }
</script>


<style>
</style>