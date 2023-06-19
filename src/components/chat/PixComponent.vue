<template>
    <div>
        <img :src="`data:image/png;base64, ${valor}`" >

    </div>
</template>

<script>
    export default{
        name: "PixComponent", 
        props: {
            valor: {
                required: true,
                type: String
            }
        }

    }
</script>