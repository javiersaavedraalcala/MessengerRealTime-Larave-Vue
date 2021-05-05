<template>
    <b-img rounded="circle" blank width="10" heigth="10" :title="online ? 'Conectado' : 'Desconectado'" :blank-color="online ? 'green' : 'gray'" ></b-img>
</template>

<script>
    export default {
        props: {
          online: Boolean,  
        },
        data() {
            return {
                
            };
        }, 
    }
</script>