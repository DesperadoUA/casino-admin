<template>
  <div>
    <v-container class="container--fluid">
      <v-row>
        <v-col class="offset-1 col-10 mt-10">
          <h1 class="page_title font-podkova-bold">Files</h1>
        </v-col>
      </v-row>
      <v-row>
          <v-col class="offset-1 col-10 mt-2 mb-5">
            <v-card>
              <v-tabs
                      v-model="tab"
                      background-color="dark"
                      dark
                      icons-and-text
                      color="white"
              >
                <v-tabs-slider></v-tabs-slider>
                <v-tab href="#tab-1" >
                  Ru <img
                        lazy-src="https://admin.onlinecasino.ua/img/ru.jpg"
                        class="lang"
                        src="https://admin.onlinecasino.ua/img/ru.jpg"
                >
                </v-tab>
                <v-tab href="#tab-2" >
                  Ua
                  <img
                          lazy-src="https://admin.onlinecasino.ua/img/ua.jpg"
                          class="lang"
                          src="https://admin.onlinecasino.ua/img/ua.jpg"
                  >
                </v-tab>
              </v-tabs>
              <v-tabs-items v-model="tab">
                <v-tab-item
                        v-for="i in 2"
                        :key="i"
                        :value="'tab-' + i"
                >
                  <v-card >
                    <v-card-text class="black">
                      <div v-if="tab == 'tab-2'">
                        <Search :postType="POST_DB" :lang="'2'" />
                        <CategoryLoop :data="postsUa" />
                        <TotalPosts :data="data.ua.total" />
                        <MM_Paginations :length = "Math.ceil(data.ua.total/numnerPostOnPage)"
                                        :lang = "2"
                                        :action = 'STORE_DIR + "/setPaginationPage"'
                                        :numberOnPage = "numnerPostOnPage"
                                        :getterPage = "STORE_DIR + '/getPage'"
                        />
                      </div>
                      <div v-else>
                        <Search :postType="POST_DB" :lang="'1'" />
                        <CategoryLoop :data="postsRu" />
                        <TotalPosts :data="data.ru.total" />
                        <MM_Paginations :length = "Math.ceil(data.ru.total/numnerPostOnPage)" 
                                        :lang = "1"
                                        :action = 'STORE_DIR + "/setPaginationPage"'
                                        :numberOnPage = "numnerPostOnPage"
                                        :getterPage = "STORE_DIR + '/getPage'"
                        />
                      </div>
                    </v-card-text>
                  </v-card>
                </v-tab-item>
              </v-tabs-items>
            </v-card>
          </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
  import Guards from '~/guards'
  import CategoryLoop from '~/components/templates/categoryLoop'
  import TotalPosts from '~/components/templates/totalPosts'
  import MM_Paginations from '~/components/lib/MM_Paginations'
  import Search from '~/components/templates/search.vue'
    export default {
        name: "admin",
        components: {CategoryLoop, TotalPosts, MM_Paginations, Search, Guards},
        middleware: ['checkAuth'],
        layout: 'admin',
        async mounted() {
            this.data.ru.posts = []
            this.data.ua.posts = []
            const user = this.$store.getters['user/getUser']
            if(!Guards.checkRouts(this.guard, user.role)) this.$router.replace('/')
            const page = this.$store.getters[this.STORE_DIR + '/getPage']
            const dataRu = {
                session: user.session,
                id: user.id,
                lang: 1,
                limit: this.numnerPostOnPage,
                offset: (page.ru - 1) * this.numnerPostOnPage
            }
            await this.$store.dispatch(this.STORE_DIR + '/setPosts', dataRu)
            const dataUa = {
                session: user.session,
                id: user.id,
                lang: 2,
                limit: this.numnerPostOnPage,
                offset: (page.ua - 1) * this.numnerPostOnPage
            }
            await this.$store.dispatch(this.STORE_DIR + '/setPosts', dataUa)
            const list = this.$store.getters[this.STORE_DIR + '/getPosts']
            this.data.ru.posts = list.ru
            this.data.ua.posts = list.ua

            const total = this.$store.getters[this.STORE_DIR + '/getTotal']
            this.data.ru.total = total.ru
            this.data.ua.total = total.ua
        
        },
        data(){
          return {
              STORE_DIR: 'files/post',
              POST_DB: 'files',
              data: {
                  ru: {
                      post_slug: 'file',
                      lang: 'ru',
                      posts: [],
                      total: 0
                  },
                  ua: {
                      post_slug: 'file',
                      lang: 'ua',
                      posts: [],
                      total: 0
                  }
              },
              tab: null,
              numnerPostOnPage: 8,
              guard: 'file'
          }
        },
        computed: {
          postsRu() {
             const list = this.$store.getters[this.STORE_DIR + '/getPosts']
             this.data.ru.posts = list.ru
             return this.data.ru.posts
          },
          postsUa() {
             const list = this.$store.getters[this.STORE_DIR + '/getPosts']
             this.data.ua.posts = list.ua
             return this.data.ua.posts
          }
        }
    }
</script>

<style scoped>

</style>