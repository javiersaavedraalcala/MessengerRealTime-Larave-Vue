<template>
    <b-row class="h-100">
        <b-col cols="8" class="h-100">
            <b-card no-body
                footer-bg-variant="light"
                footer-border-variant="dark"
                title="Conversación activa"
                class="h-100">   
                
                <b-card-body class="card-scroll">
                    <message-conversation-component 
                        v-for="message in messages" 
                        :key="message.id" 
                        :written-by-me="message.written_by_me"
                        :image="message.written_by_me ? myImage : contactImage">
                        {{ message.content }} 
                    </message-conversation-component> 
                </b-card-body> 
                
                <div slot="footer">
                    <b-form class="mb-0" @submit.prevent="postMessage">
                        <b-input-group>
                            <b-form-input class="text-center"
                                type="text"
                                v-model="newMessage"
                                autocomplete="off"
                                placeholder="Escribe un mensaje...">
                            </b-form-input>
                            <b-input-group-append>
                                <b-button variant="info" type="submit">Enviar</b-button>
                            </b-input-group-append>
                        </b-input-group>
                    </b-form>
                </div>
            </b-card>
        </b-col>
        <b-col cols="4">
            <b-img :src="contactImage" rounded="circle" width="60" heigth="60" class="m-1"></b-img>
            <p>{{contactName}}</p>
            <hr>
            <b-form-checkbox>
                Desactivar notificaciones
            </b-form-checkbox>
        </b-col>
    </b-row>
</template>

<style>
    .card-scroll {
        max-height: calc(87vh - 63px);
        overflow-y: auto;
    }
</style> 

<script>
export default {
    props: {
        contactId: Number,
        contactName: String,
        messages: Array,
        contactImage: String,
        myImage: String
    },
    data() {
        return {
            newMessage: '', 
        };
    },
    mounted() {
    },
    methods: {
        postMessage() {
            const params = {
                to_id: this.contactId,
                content: this.newMessage
            };

            axios.post('/api/messages', params)
            .then((response) => {
                if(response.data.success) {
                    this.newMessage = '';
                    const message = response.data.message;
                    message.written_by_me = true;
                    this.$emit('messageCreated', message);
                }
            });
        },
        scrollToBottom() {
            const el = document.querySelector('.card-scroll');
            el.scrollTop = el.scrollHeight;
        }
    },
    watch: {
        // contactId(value) {
        //     this.getMessages();
        // }
    },
    updated() {
        this.scrollToBottom();
    }
} 
</script>