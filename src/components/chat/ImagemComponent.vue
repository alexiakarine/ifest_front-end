<template>
    <div>
        <img :src="valor" style="width:100%; height: auto;"> 
        <p>
            {{ legenda }}
        </p>
    </div>
</template>

<script>
    export default{
        name: "ImagemComponent", 
        props: {
            valor: {
                required: true,
                type: String
            },
            legenda:{
                required: true,
                type: String
            }
        }

    }
</script>

<style scoped>
  p{
    padding-bottom: 20px;
    font-size: 14px;
    font-weight: bold;
    font-style: italic;
  }
</style>