<template>
<section class="text-gray-600 body-font overflow-hidden">

  <div class="flex justify-center">
    <div class="flex justify-center rounded-2xl bg-green-500">

      <div 
        class="w-52 h-64 m-auto bg-center bg-contain bg-no-repeat"
        :style=" 'background-image: url(' + work.fields.image.fields.file.url + ')' ">
      </div>

      <div class="w-52 h-64 flex-col flex justify-center items-start m-3 text-white">
        <p class="text-center text-xl">{{ work.fields.title }}</p>
        <p class="text-center text-sm">{{ work.fields.category.fields.name }}</p>
        <p class="text-center text-sm">{{ formatDate(work.fields.date) }}</p>
      </div>
    </div>
  </div>

  <div class="container px-5 py-24 mx-auto">
    <div class="-my-8 divide-y-2 divide-gray-100">

      <div class="py-8 flex flex-wrap md:flex-nowrap">
        <div class="md:w-64 md:mb-0 mb-6 flex-shrink-0 flex flex-col">
          <span class="font-semibold title-font text-gray-700">Predicting</span>
        </div>
        <div class="md:flex-grow">
          <p class="leading-relaxed" v-html="work.fields.predicting"></p>
        </div>
      </div>

      <div class="py-8 flex flex-wrap md:flex-nowrap">
        <div class="md:w-64 md:mb-0 mb-6 flex-shrink-0 flex flex-col">
          <span class="font-semibold title-font text-gray-700">summarizing</span>
        </div>
        <div class="md:flex-grow">
          <p class="leading-relaxed" v-html="work.fields.summarizing"></p>
        </div>
      </div>

      <div class="py-8 flex flex-wrap md:flex-nowrap">
        <div class="md:w-64 md:mb-0 mb-6 flex-shrink-0 flex flex-col">
          <span class="font-semibold title-font text-gray-700">questioning</span>
        </div>
        <div class="md:flex-grow">
          <p class="leading-relaxed" v-html="work.fields.questioning"></p>
        </div>
      </div>

    </div>
  </div>
</section>
</template>

<script>
import { createClient } from '~/plugins/contentful.js'
const client = createClient()
export default { 
  methods: {
    formatDate(date) {
      return date.split('T')[0].split('-').map(Number).join('/');
    },
  },
  // ページ コンポーネントにのみ配置できる。ローディングプレースホルダーを表示しないが、ルートナビゲーションが解決されるまでそれをブロックし、失敗するとエラーページを表示する。
  asyncData({params}) {
    return Promise.all([
      client.getEntries({
        'content_type': 'work',
        'fields.slug': params.slug
      })
    ]).then(([works]) => {
      return {
        work: works.items[0]
      }
    }).catch(console.error)
  }
}
</script>