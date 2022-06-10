<template>
   <div class="row btn_rodape justify-content-end">
        <div class="col-auto">
            <button type="button" class="btn btn-outline-secondary">Voltar</button>            
            <button type="submit" class="btn btn-primary">Enviar documentos</button>
        </div>
    </div>
</template>



<script>
    export default {
        props:[],

        methods:{
            enviarDocumentos() {
                let formulario = document.getElementById("form_signatarios");
                formulario.submit();
            }        
        }
    }
</script>


<style>
    .btn_rodape{
        margin: 2rem 0;
    }
</style>