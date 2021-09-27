<template>
  <div class="container max-w-6xl mx-auto mt-48 sm:px-6 lg:px-8">
      <div class="flex justify-center items-center bg-teal-200 h-56">
          <span class="text-gray-700 text-5xl">Friendzy</span>
      </div>
  </div>
</template>

<script>
export default {
    middleware: 'guest',
    head: {
        title: '',
    },
}
</script>
