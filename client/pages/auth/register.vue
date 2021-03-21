<template>
    <div class="container mx-auto mt-16 sm:px-6 lg:px-8">
        <form @submit.prevent="register" class="bg-teal-500 rounded mx-auto px-6 py-6 w-1/2">
            <div class="flex flex-col">
                <label for="name" class="text-white text-xl">Name</label>
                <input type="text" v-model="form.name" class="px-2 py-1 rounded" placeholder="Name">
                <span class="text-red-200 italic" v-if="errors.name">{{ errors.name[0] }}</span>
            </div>
            <div class="flex flex-col mt-3">
                <label for="username" class="text-white text-xl">Username</label>
                <input type="text" v-model="form.username" class="px-2 py-1 rounded" placeholder="Username">
                <span class="text-red-200 italic" v-if="errors.username">{{ errors.username[0] }}</span>
            </div>
            <div class="flex flex-col mt-3">
                <label for="email" class="text-white text-xl">Email</label>
                <input type="email" v-model="form.email" class="px-2 py-1 rounded" placeholder="Email">
                <span class="text-red-200 italic" v-if="errors.email">{{ errors.email[0] }}</span>
            </div>
            <div class="flex flex-col mt-3">
                <label for="password" class="text-white text-xl">Password</label>
                <input type="password" v-model="form.password" class="px-2 py-1 rounded" placeholder="Password">
                <span class="text-red-200 italic" v-if="errors.password">{{ errors.password[0]}}</span>
            </div>
            <div class="flex flex-col mt-3">
                <label for="password_confirmation" class="text-white text-xl">Confirm Password</label>
                <input type="password" v-model="form.password_confirmation" class="px-2 py-1 rounded" placeholder="Confirm Password">
            </div>
            <div class="text-center mt-3">
                <teal-button type="submit">Register</teal-button>
            </div>
        </form>
    </div>
</template>

<script>
    export default {
        middleware: 'guest',
        head: {
            title: ' | Register',
            meta: [
                { hid: 'description', name: 'description', content: 'Registration page' }
            ],
        },
        data: ()=> ({
            form: {
                name: '',
                username: '',
                email: '',
                password: '',
                password_confirmation: '',
            },
            errors: [],
        }),
        methods: {
            async register() {
                try {
                    let errors = []
                    await this.$axios.$get('sanctum/csrf-cookie')
                    await this.$axios.$post('/register', this.form)
                        .then((resp) => {})
                        .catch((err) => {
                            if (err.response.status = 422) {
                                errors = err.response.data.errors
                            }
                        })
                        this.errors = errors
                    await this.$auth.loginWith('laravelSanctum', {data: this.form})
                } catch (error) {}
            }
        }
    }
</script>
