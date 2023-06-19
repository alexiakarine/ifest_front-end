<template>
    <div>
        <a @click="colar">
            {{ valor }}
        </a>
    </div>
</template>

<script>
    export default{
        name: "CopiarComponent", 
        props: {
            valor: {
                required: true,
                type: String
            },
            texto_copiar:{
                required: true,
                type: String
            }
        },
        methods:{
            colar(){
                this.$emit('copiar-texto', this.texto_copiar); 
                console.log(this.texto_copiar)
            }
        }

    }
</script>