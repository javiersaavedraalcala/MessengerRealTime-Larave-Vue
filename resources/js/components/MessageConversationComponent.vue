<template>
    <b-media vertical-align="center" class="mb-2" :right-align="writtenByMe">
        <template #aside>
            <b-img :src="image" rounded="circle" width="48" heigth="48" class="m-1"></b-img>
        </template>
        <b-card>
            <slot></slot>
        </b-card>
    </b-media> 
</template>

<script>
    export default {
        props: {
            writtenByMe: Boolean,
            image: String
        },
        data() {
            return {
                content: 'abc'
            }
        } 
    }
</script>