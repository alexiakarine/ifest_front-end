<template>
    <div>
        <img style=" width: 100%;" :src="`data:image/png;base64, ${valor}`">
        <button class=".btn-copy">Copiar pix</button>

    </div>
</template>

<script>
import Clipboard from 'clipboard';

    export default{
        name: "PixComponent", 
        props: {
            valor: {
                required: true,
                type: String
            },
            copia_cola:{
                required: true,
                type: String
            }
        },
        mounted() {
            new Clipboard('.btn-copy', {
                text: function() {
                return this.copia_cola
                }
                })
        },
        methods:{
            copiar(){
                new Clipboard('.btn-copy', {
                    text: function() {
                        return this.copia_cola
                    }
                }).on('success', function() {
                    alert('Chave PIX copiada para a área de transferência')
                })
    
            }   
        }

    }
</script>

<style scoped>
    .btn-copy{
        background: #5f023171;
        color: black;
        border: none;
        padding: 5px;
        width: 100%;
        margin-top: 10px;
    }
       
</style>