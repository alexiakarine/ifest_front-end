<template>
    <div>
        <img style=" width: 100%;" :src="`data:image/png;base64, ${valor}`">
        <textarea v-model="copia_cola" rows=1 ref="linda"></textarea>
        <button @click="copiar" class="btn-copy">Copiar pix</button>

    </div>
</template>

<script>
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
        },
        methods:{
            copiar(){
                this.$refs.linda.select();
                document.execCommand("copy");
                alert('Chave PIX copiada para a área de transferência')
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
    textarea{
        text-overflow: ellipsis;
        width: 100%;
        resize: none;
    }
       
</style>