<template>
  <div>
    <nav
      class="
        relative
        flex flex-wrap
        items-center
        justify-between
        px-2
        py-3
        bg-green-500
        mb-3
      "
    >
      <div
        class="
          container
          px-4
          mx-auto
          flex flex-wrap
          items-center
          justify-between
        "
      >
        <div
          class="
            w-full
            relative
            flex
            justify-between
            lg:w-auto
            px-4
            lg:static lg:block lg:justify-start
          "
        >
          <nuxt-link to="/">
            <a
              class="
                text-sm
                font-bold
                leading-relaxed
                inline-block
                mr-4
                py-2
                whitespace-nowrap
                uppercase
                text-white
              "
            >
              俺の読書記録
            </a>
          </nuxt-link>
        </div>

        <!-- 検索フォーム -->
        <div id="example-navbar-warning" class="lg:flex flex items-center w-60">
          <input
            v-model="keyword"
            type="text"
            placeholder="検索はこちら"
            class="bg-gray-300 p-2 text-xs rounded w-full focus:outline-none"
            @keypress.enter="$router.push('/search/' + keyword)"
          />
        </div>
      </div>
    </nav>

    <!-- カテゴリ一覧 -->

    <div class="flex flex-wrap">
      <div class="w-full">
        <ul class="flex mb-0 list-none flex-wrap pt-3 pb-4 flex-row">
          <li class="-mb-px mr-2 last:mr-0 flex-auto text-center">
            <nuxt-link :to="'/'">
              <a
                class="
                  text-xs
                  font-bold
                  uppercase
                  px-5
                  py-3
                  shadow-lg
                  rounded
                  block
                  leading-normal
                "
                :class="{
                  'text-regal-blue bg-white': openTab !== 1,
                  'text-white bg-regal-blue': openTab === 1,
                }"
                @click="toggleTabs(1)"
              >
                all
              </a>
            </nuxt-link>
          </li>
          <li class="-mb-px mr-2 last:mr-0 flex-auto text-center">
            <nuxt-link :to="'/category/' + '6Xgdju8F9aiLfpJSok9cMr'">
              <a
                class="
                  text-xs
                  font-bold
                  uppercase
                  px-5
                  py-3
                  shadow-lg
                  rounded
                  block
                  leading-normal
                "
                :class="{
                  'text-regal-blue bg-white': openTab !== 2,
                  'text-white bg-regal-blue': openTab === 2,
                }"
                @click="toggleTabs(2)"
              >
                Self-enlightenment
              </a>
            </nuxt-link>
          </li>
          <li class="-mb-px mr-2 last:mr-0 flex-auto text-center">
            <nuxt-link :to="'/category/' + '6zShOSjkZ3a9OTotLw2MdO'">
              <a
                class="
                  text-xs
                  font-bold
                  uppercase
                  px-5
                  py-3
                  shadow-lg
                  rounded
                  block
                  leading-normal
                "
                :class="{
                  'text-regal-blue bg-white': openTab !== 3,
                  'text-white bg-regal-blue': openTab === 3,
                }"
                @click="toggleTabs(3)"
              >
                psychology
              </a>
            </nuxt-link>
          </li>
          <li class="-mb-px mr-2 last:mr-0 flex-auto text-center">
            <nuxt-link :to="'/category/' + '4SLOrm6YQyHOvukFEoekCn'">
              <a
                class="
                  text-xs
                  font-bold
                  uppercase
                  px-5
                  py-3
                  shadow-lg
                  rounded
                  block
                  leading-normal
                "
                :class="{
                  'text-regal-blue bg-white': openTab !== 4,
                  'text-white bg-regal-blue': openTab === 4,
                }"
                @click="toggleTabs(4)"
              >
                bussiness
              </a>
            </nuxt-link>
          </li>
          <li class="-mb-px mr-2 last:mr-0 flex-auto text-center">
            <a
              class="
                text-xs
                font-bold
                uppercase
                px-5
                py-3
                shadow-lg
                rounded
                block
                leading-normal
              "
              :class="{
                'text-regal-blue bg-white': openTab !== 5,
                'text-white bg-regal-blue': openTab === 5,
              }"
              @click="toggleTabs(5)"
            >
              manga
            </a>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import { createClient } from '~/plugins/contentful.js'
const client = createClient()

export default {
  name: 'PinkTabs',
  asyncData({ params }) {
    return Promise.all([
      client.getEntries({
        content_type: 'work',
        'fields.category.sys.id': params.id,
        order: '-sys.createdAt',
      }),
    ])
      .then(([works]) => {
        return {
          works: works.items, // 取得したデータを配列worksに入れる
        }
      })
      .catch(console.error)
  },
  data() {
    return {
      openTab: 1,
      keyword: '', // 変数keywordを用意し、v-model="keyword"で入力されたワードがこの中に入るようにする。
    }
  },
  methods: {
    toggleTabs(tabNumber) {
      this.openTab = tabNumber
    },
  },
}
</script>

<style></style>
