<template>
    <div class="container mx-auto mt-16">
        <div class="flex space-x-6 mx-auto w-1/2">
            <h2 class="flex-shrink-0 text-3xl">Users</h2>
            <div class="flex-1 border-l mt-3">
                <div v-for="user in users" :key="user.id" class="flex mb-3 ml-3">
                    <img src="https://images.unsplash.com/photo-1511367461989-f85a21fda167?ixid=MXwxMjA3fDB8MHxzZWFyY2h8MXx8c2lsaG91ZXR0ZXxlbnwwfHwwfA%3D%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60" alt="" class="w-8 h-8 rounded-full object-cover">
                    <NuxtLink :to="`/users/${user.id}`" class="text-xl ml-2">{{ user.username }}</NuxtLink>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        middleware: 'auth',
        data:() => ({
            users: []
        }),
        mounted() {
            this.getUsers()
        },
        methods: {
            getUsers() {
                this.$axios.$get('/api/users')
                    .then((resp) => {
                        this.users = resp.users
                    })
                    .catch((err) => {console.log(err)})
            }
        }
    }
</script>
