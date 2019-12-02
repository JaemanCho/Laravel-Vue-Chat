<template>
    <div class="flex-1">
        {{ chatId }}
    </div>
</template>

<script>
    export default {
        props: {
            chatId: {
                type: Number,
                required: true
            }
        }
    }
</script>
