<template>
    <div class="w-1/5 border-r-2 border-solid border-gray-600">
        <div v-for="user in users" :key="user.id">
            {{ user.name }}
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                users: []
            }
        },
        created() {
            axios.get('/api/users').then(res => {
                console.log(res);
                this.users = res.data.users;
            }).catch(error => {
                console.log(error);
            });
        },
        mounted() {
            console.log('ChatUserList Component mounted.')
        }
    }
</script>
