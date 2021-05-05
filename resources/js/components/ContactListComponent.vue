<template>
    <b-list-group>
        <contact-component 
            v-for="item in conversations" 
            :key="item.id" 
            :conversation="item"
            :selected="selectedConversationId === item.id"
            @click.native="selectConversation(item)">
        </contact-component>
    </b-list-group>
</template>

<script>
export default {
    props: {
        conversations: Array
    },
    data() {
        return {
            selectedConversationId: null
        };
    },
    mounted() {
    },
    methods: {
        selectConversation(conversation) {
            this.selectedConversationId = conversation.id;
            this.$emit('conversationSelected', conversation);
        }
    }
}
</script>

 