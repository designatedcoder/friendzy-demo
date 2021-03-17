<template>
    <div class="bg-teal-500 text-white text-md">
        <nav class="container flex justify-between items-center mx-auto py-5">
            <span class="font-semibold text-2xl">Friendzy</span>
            <div class="spaxe-x-2">
                <template>
                    <span>Welcome,
                        <NuxtLink to="#" class="hover:text-teal-200">
                            USERNAME
                        </NuxtLink>
                    </span>
                        <NuxtLink to="#" class="hover:text-teal-200">
                            FRIENDS
                        </NuxtLink>
                        <NuxtLink to="#" class="hover:text-teal-200">
                            USERS
                        </NuxtLink>
                        <NuxtLink to="/dashboard" class="hover:text-teal-200">
                            DASHBOARD
                        </NuxtLink>
                        <a href="#" class="">LOGOUT</a>
                </template>
                <template>
                    <NuxtLink to="/auth/register" class="hover:text-teal-200">
                        REGISTER
                    </NuxtLink>
                    <NuxtLink to="/auth/login" class="hover:text-teal-200">
                        LOGIN
                    </NuxtLink>
                </template>
            </div>
        </nav>
    </div>
</template>

<script>
    export default {

    }
</script>
