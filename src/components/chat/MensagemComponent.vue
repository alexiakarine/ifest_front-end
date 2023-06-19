<template>
    <div ref="mensagemComponent" :class="this.persona">
    </div>
</template>

<script>
import TextoComponent from './TextoComponent.vue';
import ImagemComponent from './ImagemComponent.vue';
import CopiarComponent from './CopiarComponent.vue';
import PixComponent from './PixComponent.vue';
import Vue from 'vue';

    export default{
        name: "MensagemComponent", 
        props: {
            componentes: {
                required: true,
                type: Array,
            },
            persona:{
                required: true,
                type: String
            }
            
        },
        mounted(){
            console.log(this.componentes)
            for(let componente of this.componentes){
                let vueComponente;
                if (componente.tipo == "texto"){
                    vueComponente = TextoComponent;
                }
                if (componente.tipo == "imagem"){
                    vueComponente = ImagemComponent;
                }
                if (componente.tipo == "copiar"){
                    vueComponente = CopiarComponent;
                }
                if (componente.tipo == "pix"){
                    vueComponente = PixComponent;
                }
                const instanciaComponente = new Vue({
                        render: aham => aham(
                            vueComponente,{
                                props: componente
                            }
                        )
                });
                instanciaComponente.$mount();
                this.$on('copiar-texto', this.copiarTexto);
                this.$refs.mensagemComponent.appendChild(instanciaComponente.$el);
            } 
        },
        methods:{
            copiarTexto(texto){
                console.log(texto)
                this.$emit('copiar-texto', texto);
            }
        }

    }
</script>

<style scoped>
.usuario.bot{
    width: 100%; 
    display: flex; 
    justify-content: flex-end;
}

.bot{
    background:rgb(196, 188, 193) ;
    width: max-content;
    padding: 3px;
    border-radius: 5px;
    margin-left: 5px;
    margin-top: 5px;
    max-width: 218px;
    text-align: start;
    display: flex;
    flex-direction: column;
}

.user{
    max-width: 218px;
    right: 0px;
    position: relative;
    background:rgb(245, 244, 244) ;
    width: max-content;
    right: 0;
    padding: 3px;
    border-radius: 5px;
    margin-left: 5px;
    margin-top: 5px;
    justify-self: flex-end;
    text-align: start;
    display: flex;
    flex-direction: column;
}
</style>