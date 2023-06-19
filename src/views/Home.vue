<template>
  <div class="home">
    <img class="fundo" alt="Vue logo" src="../assets/logo.jpg">
    <Button type="button" icon="pi pi-search" class="notifica" style="margin-left: 5px" @click="notificacao">
      <svg viewBox="0 0 24 24" width="24" height="24" stroke="currentColor" stroke-width="2"
       fill="none" stroke-linecap="round" stroke-linejoin="round" class="sgvNotifay">
       <path d="M18 8A6 6 0 0 0 6 8c0 7-3 9-3 9h18s-3-2-3-9"></path><path d="M13.73 21a2 2 0 0 1-3.46 0"></path>
      </svg>
    </Button>
    <div class="email">
       <h3>Feed de notícias</h3> 
       <p><br>Aceita receber e-mails com as novidades e promoções. 
       </p> 
       <input type="checkbox" id="switch" v-model= "estado"/><label for="switch">Toggle</label> 
       <br>
       <button class="aceite" @click="concordaEmail()">Concordo</button>
    </div> 
  
    <div class="chat">
        <div id="conversa" class="areaTexto">
            <div class="ajuste" ref="messages" v-for="(mensagem, index) in mensagens" :key="index" >
                <MensagemComponent :persona="mensagem.persona" :componentes="mensagem.componentes" 
                @copiar-texto="(texto) => this.meuInput = texto"/>
            </div>              
        </div>           

      <div class="areaInput">
            <input  id="enviar" type="text" v-model="meuInput" placeholder="Digite sua mensagem" @keypress="verifica">
            <Button id="enviar" type="button" icon="pi pi-search" class="buttonEnviar" style="margin-left: 5px" @click="enviar">
            <svg viewBox="0 0 24 24" width="24" height="24" stroke="currentColor" 
            stroke-width="2" fill="none" stroke-linecap="round" stroke-linejoin="round" 
            class="css-i6dzq1"><line x1="22" y1="2" x2="11" y2="13"></line><polygon 
            points="22 2 15 22 11 13 2 9 22 2"></polygon></svg></Button>           
        </div>
    </div>
  </div>

</template>

<script>
import '@/css/home.css';
import axios from "axios";
import Clipboard from 'clipboard';
import MensagemComponent from '../components/chat/MensagemComponent.vue';

export default {
  name: 'Home', 
  components: {
    MensagemComponent
  },
  data() {
    return {
      estado: false,
      meuInput: '',
      meuContexto: 'geral',
      n: 0,
      mensagens: [],
      legenda: "",
      imagens:{
        "local": ["chacara.jpg", "salao.jpeg"],
        "decoracao": ["arco.jpg","bolo.jpg","kit.jpg","baloes.jpg","tecido.jpg"]
      },
    }    
  }, 
  mounted() {
  new Clipboard('.btn-copy', {
    text: function() {
      return 'sua_chave_pix'
    }
    }),
   alert("Para iniciar ou interromper o recebimento de e-mails com novidades clique no sininho.")
  },
  methods:{
    notificacao(){
      this.ativaNotificacao()
    },
    concordaEmail(){
        document.querySelector("input#enviar").disabled = false
        document.querySelector("button#enviar").disabled = false
        document.querySelector(".chat").style.display = "block" 
        document.querySelector(".email").style.display = "none"
        localStorage.setItem('concorda', true)
        axios.post('http://localhost:5000/chat/salvar', {
        nome: 'João',
        email: 'joao@email.com',
        estado: this.estado,
        data: Date() 
      })
        .then(response => console.log(response.data))
        .catch(error => console.error(error));
    },
    ativaNotificacao(){
      document.querySelector(".email").style.display = "block" 
    },  
   copyKey(mensagem) {
    new Clipboard('.btn-copy', {
      text: function() {
        return mensagem.pix.copia_cola
      }
    }).on('success', function() {
      alert('Chave PIX copiada para a área de transferência')
    })
    },
    enviar(){
      this.mensagens.push({
          componentes: [{
            tipo: "texto",
            valor: this.meuInput
          }],
          persona: "user"
      }) 
      this.receber(this.meuInput);
      this.meuInput = '';       
      this.$nextTick(this.scrollToBottom); 
    },

    async receber(recebido) {
       axios.post("http://localhost:5000/chat/", { mensagem: recebido, contexto: this.meuContexto, n: this.n, })
       .then((response) => {

        this.meuContexto = response.data.contexto
        this.n = response.data.n

        this.mensagens.push({
          componentes: response.data.resposta,
          persona: "bot"
        }) 


      })},
    verifica(e){
      if(e.key == "Enter"){
          this.enviar();
      }
    },
    scrollToBottom() {
            let lastMessage = this.$refs.messages.slice(-1)[0];

            lastMessage.scrollIntoView();
    }
}}
</script>