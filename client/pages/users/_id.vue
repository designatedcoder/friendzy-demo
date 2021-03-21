<template>
    <div class="container mx-auto mt-16">
        <div class="flex space-x-6 mx-auto">
            <div class="flex flex-col items-end w-1/3">
                <h2 class="text-3xl">{{ user.username }}</h2>

                <template v-if="friendRequestSentFrom">
                    <div class="flex">
                        <form @submit.prevent="acceptFriend">
                            <green-button type="submit">
                                Accept
                                <svg aria-hidden="true" data-prefix="fas" data-icon="user-plus" class="fill-current w-4 h-4 ml-1 text-white svg-inline--fa fa-user-plus fa-w-20" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 640 512">
                                    <path d="M624 208h-64v-64c0-8.8-7.2-16-16-16h-32c-8.8 0-16 7.2-16 16v64h-64c-8.8 0-16 7.2-16 16v32c0 8.8 7.2 16 16 16h64v64c0 8.8 7.2 16 16 16h32c8.8 0 16-7.2 16-16v-64h64c8.8 0 16-7.2 16-16v-32c0-8.8-7.2-16-16-16zm-400 48c70.7 0 128-57.3 128-128S294.7 0 224 0 96 57.3 96 128s57.3 128 128 128zm89.6 32h-16.7c-22.2 10.2-46.9 16-72.9 16s-50.6-5.8-72.9-16h-16.7C60.2 288 0 348.2 0 422.4V464c0 26.5 21.5 48 48 48h352c26.5 0 48-21.5 48-48v-41.6c0-74.2-60.2-134.4-134.4-134.4z"/>
                                </svg>
                            </green-button>
                        </form>
                        <form @submit.prevent="denyFriend" class="ml-3">
                            <red-button type="submit">
                                Ignore
                                <svg aria-hidden="true" data-prefix="fas" data-icon="user-minus" class="fill-current w-4 h-4 ml-1 text-white svg-inline--fa fa-user-minus fa-w-20" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 640 512">
                                    <path d="M624 208H432c-8.8 0-16 7.2-16 16v32c0 8.8 7.2 16 16 16h192c8.8 0 16-7.2 16-16v-32c0-8.8-7.2-16-16-16zm-400 48c70.7 0 128-57.3 128-128S294.7 0 224 0 96 57.3 96 128s57.3 128 128 128zm89.6 32h-16.7c-22.2 10.2-46.9 16-72.9 16s-50.6-5.8-72.9-16h-16.7C60.2 288 0 348.2 0 422.4V464c0 26.5 21.5 48 48 48h352c26.5 0 48-21.5 48-48v-41.6c0-74.2-60.2-134.4-134.4-134.4z"/>
                                </svg>
                            </red-button>
                        </form>
                    </div>
                </template>

                <template v-else-if="friendRequestSentTo">
                    <span>Pending</span>
                </template>

                <template v-else-if="isFriendsWith">
                    <form @submit.prevent="deleteFriend">
                        <red-button type="submit">
                            Unfriend
                            <svg aria-hidden="true" data-prefix="fas" data-icon="user-minus" class="fill-current w-4 h-4 ml-1 text-white svg-inline--fa fa-user-minus fa-w-20" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 640 512">
                                <path d="M624 208H432c-8.8 0-16 7.2-16 16v32c0 8.8 7.2 16 16 16h192c8.8 0 16-7.2 16-16v-32c0-8.8-7.2-16-16-16zm-400 48c70.7 0 128-57.3 128-128S294.7 0 224 0 96 57.3 96 128s57.3 128 128 128zm89.6 32h-16.7c-22.2 10.2-46.9 16-72.9 16s-50.6-5.8-72.9-16h-16.7C60.2 288 0 348.2 0 422.4V464c0 26.5 21.5 48 48 48h352c26.5 0 48-21.5 48-48v-41.6c0-74.2-60.2-134.4-134.4-134.4z"/>
                            </svg>
                        </red-button>
                    </form>
                </template>

                <template v-else-if="this.$auth.user.id != this.user.id">
                    <form @submit.prevent="addFriend">
                        <blue-button type="submit">
                            Add Friend
                            <svg aria-hidden="true" data-prefix="fas" data-icon="user-plus" class="fill-current w-4 h-4 ml-1 text-white svg-inline--fa fa-user-plus fa-w-20" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 640 512">
                                <path d="M624 208h-64v-64c0-8.8-7.2-16-16-16h-32c-8.8 0-16 7.2-16 16v64h-64c-8.8 0-16 7.2-16 16v32c0 8.8 7.2 16 16 16h64v64c0 8.8 7.2 16 16 16h32c8.8 0 16-7.2 16-16v-64h64c8.8 0 16-7.2 16-16v-32c0-8.8-7.2-16-16-16zm-400 48c70.7 0 128-57.3 128-128S294.7 0 224 0 96 57.3 96 128s57.3 128 128 128zm89.6 32h-16.7c-22.2 10.2-46.9 16-72.9 16s-50.6-5.8-72.9-16h-16.7C60.2 288 0 348.2 0 422.4V464c0 26.5 21.5 48 48 48h352c26.5 0 48-21.5 48-48v-41.6c0-74.2-60.2-134.4-134.4-134.4z"/>
                            </svg>
                        </blue-button>
                    </form>
                </template>
            </div>
            <div class="flex border-l mt-3 w-2/3">
                <div class="flex mb-3 ml-3">
                    <img src="https://images.unsplash.com/photo-1511367461989-f85a21fda167?ixid=MXwxMjA3fDB8MHxzZWFyY2h8MXx8c2lsaG91ZXR0ZXxlbnwwfHwwfA%3D%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60" alt="" class="w-8 h-8 rounded-full object-cover">
                    <div class="flex flex-col">
                        <span class="text-xl ml-2">{{ user.name }}</span>
                        <span class="text-xl ml-2">{{ user.email }}</span>
                        <span class="text-xl ml-2">{{ user.username }}</span>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        middleware: 'auth',
        data:() => ({
            user: {},
            isFriendsWith: '',
            friendRequestSentTo: '',
            friendRequestSentFrom: ''
        }),
        created() {
            this.getUser()
        },
        methods: {
            getUser() {
                this.$axios.$get('/api/user/'+this.$route.params.id)
                    .then((resp)=>{
                        this.user = resp.user
                        this.isFriendsWith = resp.isFriendsWith
                        this.friendRequestSentTo = resp.friendRequestSentTo
                        this.friendRequestSentFrom = resp.friendRequestSentFrom
                    })
                    .catch((err)=>{console.log(err)})
            },
            addFriend() {
                this.$axios.$post('/api/friends/'+this.$route.params.id)
                    .then((resp) => this.getUser())
                    .catch((err)=>{console.log(err)})
            },
            acceptFriend() {
                this.$axios.$patch('/api/friends/'+this.$route.params.id)
                    .then((resp) => this.getUser())
                    .catch((err)=>{console.log(err)})
            },
            denyFriend() {
                this.$axios.$get('/api/friends/'+this.$route.params.id)
                    .then((resp) => this.getUser())
                    .catch((err)=>{console.log(err)})
            },
            deleteFriend() {
                this.$axios.$delete('/api/friends/'+this.$route.params.id)
                    .then((resp) => this.getUser())
                    .catch((err)=>{console.log(err)})
            }
        }
    }
</script>
