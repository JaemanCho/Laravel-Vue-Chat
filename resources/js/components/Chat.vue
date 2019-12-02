<template>
    <div class="flex h-full">
        <ChatUserList 
            :current-user="currentUser"
            @updatedChatWith="updatedChatWith"
        />
        <div v-if="chatWith" class="w-4/5 flex flex-col">
            <ChatArea 
                :chat-id="chatWith"
            />
            <div class="flex-initial p-2">
                <input 
                    class="border-2 border-solid rounded border-gray-600 w-full p-3" 
                    type="text"
                    v-model="text"
                    @keyup.enter="submit"
                >
            </div>
        </div>
        <div v-else>
            Select a user to chat!
        </div>
    </div>
</template>

<script>
    import ChatUserList from './ChatUserList';
    import ChatArea from './ChatArea';
    export default {
        props:{
            currentUser: {
                type: Number,
                required: true
            }
        },
        data() {
            return {
                chatWith: null,
                text: ''
            }
        },
        components: {
            ChatUserList,
            ChatArea
        },
        methods: {
            updatedChatWith(value) {
                this.chatWith = value;
            },
            submit() {
                if (this.text) {
                    axios.post('/api/messages', {
                        text: this.text,
                        to: this.chatWith,
                        from: this.currentUser
                    });
                }
            }
        }        
    }
</script>