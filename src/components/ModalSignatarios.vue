<template>       
   <b-modal :id="'modal_signatario_'+signatario.email" ref="modal" hide-header-close hide-footer>

        <template #modal-header="{}">
            <h5>Alterar dados</h5>
        </template>

        <template #default="{}">
            <form method="post" onsubmit="event.preventDefault()">
            <b-alert show variant="warning">{{ signatario.email }}</b-alert>

            <b-form-group class="label_dados" label="Nome completo" :label-for="'nome_'+signatario.email" invalid-feedback="Preenchimento obrigatório">
                <b-form-input class="campo_nome" :id="'campo_nome_'+signatario.email" :value="signatario.nome" required></b-form-input>          
            </b-form-group>

            <b-form-group class="label_dados" label="Informações extras" label-for="campo_extra">
                <b-form-input class="campo_extra" :id="'campo_extra_'+signatario.email" :value="signatario.extra"></b-form-input>          
            </b-form-group>

            <div class="modal_footer">
                <button type="button" class="btn btn-secondary" v-on:click="cancelarAlteracao(signatario)">Cancelar</button>
                <button type="submit" class="btn btn-primary" v-on:click="salvarEdicao(signatario)">Salvar alterações</button>
            </div>
            </form>
        </template>
    </b-modal>

</template>

<script>
    export default {
        props:['signatario', 'signatarios', 'emails'],

        methods:{          
            removerEmail(email) {
                this.emails.splice(this.emails.indexOf(email), 1);
            },
            
            cancelarAlteracao(signatario) {
                this.$root.$emit("bv::toggle::modal", "modal_signatario_" + signatario.email);
                console.table(this.signatarios);
            },
            salvarEdicao(signatario) {
                var nome = document.getElementById("campo_nome_" + signatario.email).value;
                var extra = document.getElementById("campo_extra_" + signatario.email).value;
                if (nome.length > 0) {
                    signatario.nome = nome;
                    signatario.extra = extra;                    
                    
                    this.$root.$emit("bv::toggle::modal", "modal_signatario_" + signatario.email);
                    console.table(this.signatarios);
                }
            },

        
        }

    }
</script>



<style>
    .modal_footer{
        margin-top: 2rem;
        text-align: right;
    }
    .alert-warning{
        text-align: center;
    }
    .label_dados{
        font-weight: bold;
        margin: 0.8rem 0 0 0;
    }
</style>