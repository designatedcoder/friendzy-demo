<template>
    <div class="flex justify-around items-start container space-x-6 mx-auto mt-16">
        <div class="flex flex-col justify-center border-r w-full">
            <h2 class="text-3xl underline mb-3">Friend Requests</h2>
            <div>
                <div v-for="request in requests" :key="request.id" class="flex mb-3">
                    <img src="https://images.unsplash.com/photo-1511367461989-f85a21fda167?ixid=MXwxMjA3fDB8MHxzZWFyY2h8MXx8c2lsaG91ZXR0ZXxlbnwwfHwwfA%3D%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60" alt="" class="w-8 h-8 rounded-full object-cover">
                    <NuxtLink :to="`/users/${request.id}`" class="text-xl ml-2">
                    {{ request.username }}
                    </NuxtLink>
                </div>
            </div>
        </div>
        <div class="flex flex-col justify-center w-full">
            <h2 class="text-3xl underline mb-3">Friends</h2>
            <div>
                <div v-for="friend in friends" :key="friend.id" class="flex mb-3">
                    <img src="https://images.unsplash.com/photo-1511367461989-f85a21fda167?ixid=MXwxMjA3fDB8MHxzZWFyY2h8MXx8c2lsaG91ZXR0ZXxlbnwwfHwwfA%3D%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60" alt="" class="w-8 h-8 rounded-full object-cover">
                    <NuxtLink :to="`/users/${friend.id}`" class="text-xl ml-2">
                    {{ friend.username }}
                    </NuxtLink>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data: ()=>({
            friends: [],
            requests: [],
        }),
        mounted() {
            this.getFriends()
        },
        methods: {
            getFriends() {
                this.$axios.$get('/api/friends')
                    .then((resp) => {
                        this.friends = resp.friends
                        this.requests = resp.requests
                    })
            }
        }
    }
</script>
