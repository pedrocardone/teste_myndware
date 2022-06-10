<template>
   <div class="row linha_pedir_ordem" v-show="btn_pedir_ordem">
        <div class="col-12 offset-0 col-sm-11 offset-sm-1">
            <div class="form-check form-switch">
                <input class="form-check-input" type="checkbox" role="switch" id="switch_pedir_ordem" checked>
                <label class="form-check-label" for="switch_pedir_ordem">Pedir assinaturas nessa ordem</label>
                <div class="form-text">Se ativado, os pedidos para assinar serão enviados na ordem dos e-mails acima.</div>
            </div>
        </div>
    </div> 
</template>



<script>
    export default {
        props:['btn_pedir_ordem'],

        methods:{                
        }
    }
</script>


<style>
    .linha_pedir_ordem {
        border-top: 1px solid #ececec;
        padding: 2rem 0.5rem;
    }
    .form-switch input{
        width: 4rem !important;
        height: 2rem;
        margin-top: 0.8rem;
        margin-right: 1rem;
    }
    .form-switch label{
        font-weight: bold;
        font-size: 1.3rem;
    }
    .form-switch .form-text{
        margin: 0px;
    }

    @media (max-width: 767.98px) {       
           
        .form-switch input{
            width: 3rem !important;
            height: 1.5rem;
            margin-top: 1.5rem;
            margin-right: 1rem;
        }
        .form-switch label{
            font-weight: bold;
            font-size: 1rem;
        }
    }
    @media (max-width: 575.98px) {
        .linha_pedir_ordem{
            padding: 1.5rem 0;
        }
        
        .form-switch input{
            width: 3rem !important;
            height: 1.7rem;
            margin-top: 2.5rem;

        }
    }
</style>