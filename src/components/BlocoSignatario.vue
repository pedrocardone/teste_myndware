<template>      

    <div class="row linha_signatario" >
        <div class="col-1 col-sm-1 d-flex flex-column justify-content-center align-items-center">
            <b-icon icon="grip-vertical" class="icone_grip_vertical"></b-icon>
        </div>
        <div class="col-10 col-sm-9">
            <div class="row">
                <div class="col-12">
                    <h5>{{signatario.nome}}</h5>
                    <p>{{signatario.extra}}</p>
                    <p>{{signatario.email}}</p>
                </div>
            </div>
            <div class="row selects_signatario">
                <div class="col-12 col-sm-12 col-md-6">
                    <select class="form-select" required aria-label="Ação" v-on:change="salvaAcao(signatario, $event.target.value)">
                        <option value="">Ação</option>
                        <option value="assinar">Assinar</option>
                        <option value="reconhecer">Reconhecer</option>
                    </select>
                </div>
                <div class="col-12 col-sm-12 col-md-6">
                    <select class="form-select" required aria-label="Como deve assinar" v-on:change="salvaComoAssinar(signatario, $event.target.value)">
                        <option value="" selected>Como deve assinar?</option>
                        <option value="parte">Parte</option>
                        <option value="testemunha">Testemunha</option>
                    </select>
                </div>
            </div>
        </div>

        <div class="col-1 col-sm-2 d-flex flex-column align-items-end">
            <div>
                <b-icon icon="pencil" class="icone_pencil" v-on:click="abreModalSignatario(signatario)"></b-icon>
                <b-icon icon="trash" class="icone_trash" v-on:click="removerSignatario(signatario)"></b-icon>
            </div>
        </div>
        
        <div class="col-11 offset-1 check_notificar">                   
            <div class="form-check">
            <input class="form-check-input" type="checkbox" :id="'check_not_'+signatario.email" v-on:change="salvaRecNot(signatario, $event.target)" checked>
            <label class="form-check-label" :for="'check_not_'+signatario.email">
                Enviar notificações sobre o progresso da assinatura digital
            </label>
            </div>
        </div>
    </div>



</template>

<script>
    export default {
        props:['signatario', 'signatarios'],

        methods:{
            salvaAcao(signatario, valor) {
                signatario.acao = valor;
                console.table(this.signatarios);
            },
            salvaComoAssinar(signatario, valor) {
                signatario.como = valor;
                console.table(this.signatarios);
            },
            salvaRecNot(signatario, valor) {
                if (valor.checked) {
                    signatario.receberNotificacoes = "sim";
                }
                else {
                    signatario.receberNotificacoes = "nao";
                }
                console.table(this.signatarios);
            },
            abreModalSignatario(signatario) {
                this.$root.$emit("bv::toggle::modal", "modal_signatario_" + signatario.email);                
            },
            removerSignatario(signatario) {
                this.signatarios.splice(this.signatarios.indexOf(signatario), 1);
            }
        
        }

    }
</script>



<style>
    .linha_signatario{
        padding: 2rem 0px;
        border-top: 1px solid #ececec;
    }
    .linha_signatario h5{
        margin-bottom: 10px;
    }
    .linha_signatario p{
        display: inline-block;
        margin-right: 2rem;
        color: #5f5f5f;
    }
    .linha_signatario p:empty{
        margin: 0px;
    }
    .icone_grip_vertical{
        font-size: 1.5rem;
        color: #b3b3b3;
    }
    .icone_trash{
        font-size: 1.3rem;
        color: red;
        margin: 0 0.5rem;
        cursor: pointer;
    }
    .icone_pencil{
        font-size: 1.3rem;
        margin: 0 0.5rem;
        color: gray;
        cursor: pointer;
    }
    .check_notificar{
        font-weight: bold;
        margin-top: 0.7rem;
    }
    .check_notificar label{
        font-weight: bold;
    }


    @media (max-width: 767.98px) {        
        .selects_signatario div{
            padding: 5px 0px;
        }
        .icone_pencil, .icone_trash{
            font-size: 1rem;
            margin: 10px auto;
        } 
    }
    
</style>