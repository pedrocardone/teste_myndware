<template>    
    <b-modal :id="'modal_'+email.endereco" ref="modal" hide-header-close hide-footer>
        <template #modal-header="{}">
            <h5>Adicionar pessoa fora da organização</h5>
        </template>

        
        <template #default="{}">            
            <form method="post" onsubmit="event.preventDefault()">
                <p>Identificados X pessoas fora da organização. Insira os nomes das pessoas e informações extras como cargos ou observações.</p>
                <b-alert show variant="warning">{{ email.endereco }}</b-alert>

                <b-form-group class="label_dados" label="Nome completo" :label-for="'nome_'+email.endereco">
                    <b-form-input class="campo_nome" :id="'campo_nome_'+email.endereco" :value="email.nome" v-model="email.nome" required></b-form-input>          
                </b-form-group>

                <b-form-group class="label_dados" label="Informações extras" label-for="campo_extra">
                    <b-form-input class="campo_extra" :id="'campo_extra_'+email.endereco" :value="email.extra"></b-form-input>          
                </b-form-group>

                <div class="modal_footer">
                    <button type="button" class="btn btn-secondary" v-on:click="cancelarAdd(email)">Cancelar</button>
                    <button type="submit" class="btn btn-primary" v-on:click="ok(email)">Salvar informações</button>
                </div>
            </form>
        </template>
    </b-modal>
</template>

<script>
    export default {
        props:['email', 'signatarios', 'emails'],

        methods:{
            ok(email) {
                var nome = document.getElementById("campo_nome_"+email.endereco).value;
                var extra = document.getElementById("campo_extra_"+email.endereco).value;

                if(nome.length > 0){
                    var novo = []
                    novo.email =  email.endereco
                    novo.nome =  nome
                    novo.extra =  extra
                    novo.receberNotificacoes =  'sim'

                    this.signatarios.push(novo)
                    this.removerEmail(email)
                    this.$root.$emit('bv::toggle::modal', 'modal_'+email.endereco)
                    console.table(this.signatarios)
                }            
            },

            cancelarAdd(email){
                this.$root.$emit('bv::toggle::modal', 'modal_'+email.endereco)              
                console.table(this.signatarios)
            },
            removerEmail(email) {
                this.emails.splice(this.emails.indexOf(email), 1);
            }
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