<template>
    <div>
        <img :src="valor">
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