<template>
    <div>
        <p>
            {{ valor }}
        </p>
    </div>
</template>

<script>
    export default{
        name: "TextoComponent", 
        props: {
            tipo: {
                required: true,
                type: String
            },
            valor: {
                required: true,
                type: String
            }
        }

    }
</script>