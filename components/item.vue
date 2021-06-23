<template>
  <div class="w-52 my-3 mx-4 py-2 bg-white overflow-hidden shadow-lg">
    <div 
      class="mb-3 w-52 h-64 bg-center bg-cover"
      :style=" 'background-image: url(' + work.fields.image.fields.file.url + ')' "
    >
    </div>
    <nuxt-link :to=" '/work/' + work.fields.slug ">
      <h3 class="ml-3 font-bold">{{ work.fields.title }}</h3>
    </nuxt-link>
    <h4 class="ml-3 my-2 text-xs">{{ work.fields.category.fields.name }}</h4>
  </div>
</template>

<script>
export default {
  props: ['work']
}
</script>