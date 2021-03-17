<template>
    <button :type="type" class="inline-flex items-center justify-center px-4 py-2 bg-teal-300 border border-transparent rounded-md font-semibold text-teal-700 uppercase tracking-widest hover:bg-green-700 hover:text-gray-200 focus:outline-none focus:border-blue-700 focus:shadow-outline-blue active:bg-teal-300 transition ease-in-out duration-150">
        <slot></slot>
    </button>
</template>

<script>
    export default {
        props: {
            type: {
                type: String,
                default: 'button'
            }
        }
    }
</script>
