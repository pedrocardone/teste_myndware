<template>
    <div class="container">       
        <ModalEmail v-for="email of emails" :emails="emails" :email="email" :signatarios="signatarios"></ModalEmail>

        <ModalSignatarios v-for="signatario of signatarios" :emails="emails" :signatario="signatario" :signatarios="signatarios"></ModalSignatarios>

        <div class="row topo align-items-end" style="margin: 2rem 0 1rem 0">
            <div class="col-lg-9 col-md-8 col-sm-12 col-12 ">
                <h3>Quem precisa assinar</h3>
            </div>
            <div class="col-lg-3 col-md-4 col-sm-12 col-12">
                <a class="link_addemail" v-on:click="adicionarEmailLogado()">Adicionar meu email</a>
            </div>
        </div>

        <div class="row linha_emails">
            <span class="input-group-text campo_email col-auto" v-for="email of emails">{{email.endereco}} <b-icon icon="x-lg" class="icone_remover_email" v-b-popover.hover.bottom="'Remover esse ítem'" v-on:click="removerEmail(email)"></b-icon></span>

            <div class="col-lg-auto col-md-12 col-sm-12 col-12" style="min-width: 40%; padding: 3px 0px 0px 0px;">
                <input class="form-control" type="text" id="campo_add_email" placeholder="Adicione aqui os emails de quem deve assinar" v-on:keyup="addEmail($event.target.value)">
            </div>            
        </div>         
        
        <div class="row"> 
            <div class="col-auto" style="margin:1rem 0px;">  
                <button type="button" class="btn btn-primary" v-show="btn_add_sign" v-on:click="abreModal(false)">Adicionar signatários</button>
            </div>
        </div>

        <BlocoNenhumSign :nenhum_signatario="nenhum_signatario"></BlocoNenhumSign>


        <form method="post" onsubmit="event.preventDefault()">  
            <BlocoSignatario v-for="signatario of signatarios" :signatario="signatario" :signatarios="signatarios"></BlocoSignatario>

            <SwitchPedirOrdem :btn_pedir_ordem="btn_pedir_ordem"></SwitchPedirOrdem>    

            <BlocoRodape></BlocoRodape>
        </form>
    </div>

</template> 




<script>
    import ModalEmail from './components/ModalEmail.vue'
    import ModalSignatarios from './components/ModalSignatarios.vue';
    import BlocoSignatario from './components/BlocoSignatario.vue';
    import SwitchPedirOrdem from './components/SwitchPedirOrdem.vue';
    import BlocoRodape from './components/BlocoRodape.vue';
import BlocoNenhumSign from './components/BlocoNenhumSign.vue';

    export default {        
        components: {
    ModalEmail,
    ModalSignatarios,
    BlocoSignatario,
    SwitchPedirOrdem,
    BlocoRodape,
    BlocoNenhumSign
},

    data() {
        return {
            btn_add_sign: false,
            btn_pedir_ordem: false,
            nenhum_signatario: true,
            usuario_logado: "teste@teste.com",
            emails: [],
            signatarios: []
        };
    },
    watch: {
        emails() {
            if (this.emails.length > 0) {
                this.btn_add_sign = true;
            }
            else {
                this.btn_add_sign = false;
            }
        },
        signatarios() {
            if (this.signatarios.length > 0) {
                this.nenhum_signatario = false;
                this.btn_pedir_ordem = true;
            }
            else {
                this.nenhum_signatario = true;
                this.btn_pedir_ordem = false;
            }
        }
    },
    methods: {
        adicionarEmailLogado() {
            this.emails.push({ endereco: this.usuario_logado });
        },
        addEmail(valor) {
            let ult = valor.substr(-1);
            var valor = valor.slice(0, -1);
            ;
            if (ult == " " || ult == "," || ult == ";") {
                var regex = /\S+@\S+\.\S+/;
                if (regex.test(valor)) {
                    this.emails.unshift({ endereco: valor });
                    document.getElementById("campo_add_email").value = "";
                }
            }
        },
        removerEmail(email) {
            this.emails.splice(this.emails.indexOf(email), 1);
        },
        removerSignatario(signatario) {
            this.signatarios.splice(this.signatarios.indexOf(signatario), 1);
        },
        abreModal() {            
            for (let i = 0; i < this.emails.length; i++) {
                this.$root.$emit("bv::toggle::modal", "modal_" + this.emails[i].endereco);
            }            
        },
       
       
        
    }
}
   
     
</script>

<style>
    .topo div:last-child{
        text-align: right;
    }
    .link_addemail{
        text-decoration:none;
        font-weight:bold;
        cursor: pointer;
    }
    .link_addemail:hover{
        text-decoration:underline;
    }
    .linha_emails{
        border: 1px solid #CCCCCC;
        border-radius: 0.8rem;
        margin: 0px;
        padding: 0.5rem;
    }
    .campo_email{
        border-radius: 20px;
        margin: 3px;
        background-color: #e9ecef;
        border: none;
    }
    #campo_add_email{
        border-radius: 20px;
        border: none;
    }
    .icone_remover_email{
        margin-left: 10px;
        width: 12px;
        height: 12px;
        cursor: pointer;
    }
    .icone_remover_email:hover{
        color: red;
    }   

    @media (max-width: 575.98px) {
        .topo div:first-child, .topo div:last-child{
            text-align: center;
        }       
    }
</style>
