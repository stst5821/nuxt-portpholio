<template>
<div>
    <nav class="relative flex flex-wrap items-center justify-between px-2 py-3 bg-green-500 mb-3">
  <div class="container px-4 mx-auto flex flex-wrap items-center justify-between">
    <div class="w-full relative flex justify-between lg:w-auto  px-4 lg:static lg:block lg:justify-start">
      <nuxt-link to="/">
      <a class="text-sm font-bold leading-relaxed inline-block mr-4 py-2 whitespace-nowrap uppercase text-white">
        俺の読書記録
      </a>
      </nuxt-link>
      <button class="cursor-pointer text-xl leading-none px-3 py-1 border border-solid border-transparent rounded bg-transparent block lg:hidden outline-none focus:outline-none" type="button">
        <span class="block relative w-6 h-px rounded-sm bg-white"></span>
        <span class="block relative w-6 h-px rounded-sm bg-white mt-1"></span>
        <span class="block relative w-6 h-px rounded-sm bg-white mt-1"></span>
      </button>
    </div>
    <div class="lg:flex flex-grow items-center" id="example-navbar-warning">
      <ul class="flex flex-col lg:flex-row list-none ml-auto">
          <li class="nav-item">
            <a class="px-3 py-2 flex items-center text-xs uppercase font-bold leading-snug text-white hover:opacity-75" href="#pablo">
              about
            </a>
          </li>
          <li class="nav-item">
            <a class="px-3 py-2 flex items-center text-xs uppercase font-bold leading-snug text-white hover:opacity-75" href="#pablo">
              skills
            </a>
          </li>
          <li class="nav-item">
            <a class="px-3 py-2 flex items-center text-xs uppercase font-bold leading-snug text-white hover:opacity-75" href="#pablo">
              works
            </a>
          </li>
          <li class="nav-item">
            <a class="px-3 py-2 flex items-center text-xs uppercase font-bold leading-snug text-white hover:opacity-75" href="#pablo">
              contact
            </a>
          </li>
      </ul>
    </div>
  </div>
</nav>

<!-- カテゴリ一覧 -->

  <div class="flex flex-wrap">
    <div class="w-full">
      <ul class="flex mb-0 list-none flex-wrap pt-3 pb-4 flex-row">
        <li class="-mb-px mr-2 last:mr-0 flex-auto text-center">
          <nuxt-link :to=" '/' ">
            <a class="text-xs font-bold uppercase px-5 py-3 shadow-lg rounded block leading-normal" v-on:click="toggleTabs(1)" v-bind:class="{'text-pink-600 bg-white': openTab !== 1, 'text-white bg-pink-600': openTab === 1}">
              all
            </a>
          </nuxt-link>
        </li>
        <li class="-mb-px mr-2 last:mr-0 flex-auto text-center">
          <nuxt-link :to=" '/category/' + '6Xgdju8F9aiLfpJSok9cMr' ">
            <a class="text-xs font-bold uppercase px-5 py-3 shadow-lg rounded block leading-normal" v-on:click="toggleTabs(2)" v-bind:class="{'text-pink-600 bg-white': openTab !== 2, 'text-white bg-pink-600': openTab === 2}">
              Self-enlightenment
            </a>
          </nuxt-link>
        </li>
        <li class="-mb-px mr-2 last:mr-0 flex-auto text-center">
          <nuxt-link :to=" '/category/' + '6zShOSjkZ3a9OTotLw2MdO' ">
            <a class="text-xs font-bold uppercase px-5 py-3 shadow-lg rounded block leading-normal" v-on:click="toggleTabs(3)" v-bind:class="{'text-pink-600 bg-white': openTab !== 3, 'text-white bg-pink-600': openTab === 3}">
              psychology
            </a>
          </nuxt-link>
        </li>
        <li class="-mb-px mr-2 last:mr-0 flex-auto text-center">
    <nuxt-link :to=" '/category/' + '4SLOrm6YQyHOvukFEoekCn' ">
          <a class="text-xs font-bold uppercase px-5 py-3 shadow-lg rounded block leading-normal" v-on:click="toggleTabs(4)" v-bind:class="{'text-pink-600 bg-white': openTab !== 4, 'text-white bg-pink-600': openTab === 4}">
            bussiness
          </a>
    </nuxt-link>
        </li>
        <li class="-mb-px mr-2 last:mr-0 flex-auto text-center">
          <a class="text-xs font-bold uppercase px-5 py-3 shadow-lg rounded block leading-normal" v-on:click="toggleTabs(5)" v-bind:class="{'text-pink-600 bg-white': openTab !== 5, 'text-white bg-pink-600': openTab === 5}">
            manga
          </a>
        </li>
      </ul>
    </div>
  </div>
</div>


</template>

<script>
import About from "~/components/about.vue";
import Item from '@/components/Item' // ここを追加
import { createClient } from '~/plugins/contentful.js'
const client = createClient()

export default {
  components: {
    Item
  },
  asyncData ({params}) {
    return Promise.all([
      client.getEntries({
        'content_type': 'work',
        'fields.category.sys.id': params.id,
        order: '-sys.createdAt'
      }),
    ]).then(([works]) => {
      return {
        works: works.items // 取得したデータを配列worksに入れる
      }
    }).catch(console.error)
  },
  name: "pink-tabs",
  data() {
    return {
      openTab: 1
    }
  },
  methods: {
    toggleTabs: function(tabNumber){
      this.openTab = tabNumber
    }
  }
};
</script>

<style>
</style>