<template>
  <div>
    <v-app-bar app dark >
      <v-app-bar-nav-icon
              @click="drawer = !drawer"
      >
      </v-app-bar-nav-icon>
      <v-spacer></v-spacer>
      <v-toolbar-items class="hidden-sm-and-down">
        <v-btn text exact
               class="font-podkova-bold nav-link"
               v-for="link in links"
               :key="link.title" 
               :to="link.url"
        >
          {{link.title}}
        </v-btn>
        <v-btn text exact
               class="font-podkova-bold nav-link"
               @click="logout"
               no-prefetch
        >
          LOGOUT
        </v-btn>
      </v-toolbar-items>
    </v-app-bar>
    <v-navigation-drawer app temporary
                         v-model="drawer" 
                         class="grey darken-4" 
                         color="deep-orange darken-2">
      <v-container>
        <v-layout class="mt-5" wrap>
          <v-btn
           v-for="link in commonLinks"
               :key="link.title" :to="link.url"
                  class="deep-orange darken-2 justify-start display_block mb-2 font-podkova-bold"
                  dark
                  exact
                  no-prefetch>
            <v-icon left color="white">{{link.icon}}</v-icon>
            {{link.title}}
          </v-btn>
          <v-menu
                  transition="slide-y-transition"
                  bottom
                  no-prefetch
                  class="d-block"
                  v-for="item in postTypes" 
                  :key="item.title"
          >
            <template v-slot:activator="{ on, attrs }">
              <v-btn
                      class="deep-orange darken-2 justify-start display_block font-podkova-bold mb-2"
                      dark
                      v-bind="attrs"
                      v-on="on"
              >
                <v-icon left>mdi-folder-multiple-outline</v-icon>
               {{item.title}}
              </v-btn>
            </template>
            <v-list>
              <v-list-item
                      no-prefetch
                      class="font-podkova-bold"
                      v-for="(link, i) in item.links"
                      :key="i" :to="link.url"
              >
                <v-list-item-title>
                  {{ link.title }}
                </v-list-item-title>
              </v-list-item>
            </v-list>
          </v-menu>
        </v-layout>
        <v-layout class="justify-space-around align-center">
          <v-btn class="deep-orange darken-2 display_block justify-start" color="deep-orange darken-2 font-podkova-bold"
                 @click="logout">
            <v-icon left color="white">mdi-logout</v-icon>
            Logout
          </v-btn>
        </v-layout>
      </v-container>
    </v-navigation-drawer>
  </div>
</template>

<script>
    import Guards from '~/guards'
    const commonLinks = [
      {title:'MAIN', url:'/admin', icon:'mdi-bank', type: 'common'},
      {title:'SETTINGS', url:'/admin/settings', icon:'mdi-message-draw', type: 'setting'},
      {title:'STATIC PAGES', url:'/admin/static-pages', icon:'mdi-checkbox-multiple-blank', type: 'page'},
      {title:'OPTIONS', url:'/admin/options', icon:'mdi-share-variant', type: 'option'}
    ]
    export default {
        name: "AdminMenu",
        data(){
            return {
                drawer: false,
                commonLinks: commonLinks,
                links: [
                  ...commonLinks,
                  {title:'CASINO', url:'/admin/casino', icon:'mdi-cash-usd', type: 'casino'},
                  {title:'GAMES', url:'/admin/game', icon:'mdi-gamepad-variant', type: 'game'},
                  {title:'LICENSES', url:'/admin/license', icon:'mdi-gamepad-variant', type: 'license'},
                  {title:'ARTICLE', url:'/admin/article', icon:'mdi-gamepad-variant', type: 'article'},
                  {title:'PAYMENT', url:'/admin/payment', icon:'mdi-gamepad-variant', type: 'payment'},
                  {title:'VENDOR', url:'/admin/vendor', icon:'mdi-gamepad-variant', type: 'vendor'},
                  {title:'Bonus', url:'/admin/bonus', icon:'mdi-gamepad-variant', type: 'bonus'}
                ],
                postTypes: [
                  {
                    title: 'Casinos',
                    type: 'casino',
                    links: [
                      { title: 'All casino', url: '/admin/casino'},
                      { title: 'Add casino', url: '/admin/casino/add'},
                      { title: 'All category casino', url: '/admin/casino/category'},
                      { title: 'Add category casino', url: '/admin/casino/category/add'}
                    ]
                  },
                  {
                    title: 'Games',
                    type: 'game',
                    links: [
                      { title: 'All games', url: '/admin/game' },
                      { title: 'Add games', url: '/admin/game/add' },
                      { title: 'All category games', url: '/admin/game/category' },
                      { title: 'Add category games', url: '/admin/game/category/add' }
                    ]
                  },
                  {
                    title: 'License',
                    type: 'license',
                    links: [
                      { title: 'All license', url: '/admin/license' },
                      { title: 'Add license', url: '/admin/license/add' },
                      { title: 'All category license', url: '/admin/license/category' },
                      { title: 'Add category license', url: '/admin/license/category/add' }
                    ]
                  },
                  {
                    title: 'Article',
                    type: 'article',
                    links: [
                      { title: 'All article', url: '/admin/article' },
                      { title: 'Add article', url: '/admin/article/add' },
                      { title: 'All category article', url: '/admin/article/category' },
                      { title: 'Add category article', url: '/admin/article/category/add' }
                    ]
                  },
                  {
                    title: 'Payment',
                    type: 'payment',
                    links: [
                      { title: 'All payments', url: '/admin/payment' },
                      { title: 'Add payment', url: '/admin/payment/add' },
                      { title: 'All category payment', url: '/admin/payment/category' },
                      { title: 'Add category payment', url: '/admin/payment/category/add' }
                    ]
                  },
                  {
                    title: 'Vendor',
                    type: 'vendor',
                    links: [
                      { title: 'All vendors', url: '/admin/vendor' },
                      { title: 'Add vendor', url: '/admin/vendor/add' },
                      { title: 'All category vendor', url: '/admin/vendor/category' },
                      { title: 'Add category vendor', url: '/admin/vendor/category/add' }
                    ]
                  },
                  {
                    title: 'Bonus',
                    type: 'Bonus',
                    links: [
                      { title: 'All bonus', url: '/admin/bonus' },
                      { title: 'Add bonus', url: '/admin/bonus/add' },
                      { title: 'All category bonus', url: '/admin/bonus/category' },
                      { title: 'Add category bonus', url: '/admin/bonus/category/add' }
                    ]
                  }
                ]
            }
        },
        mounted(){
          const user = this.$store.getters['user/getUser']
          this.commonLinks = Guards.checkLinks(this.commonLinks, user.role)
          this.links = Guards.checkLinks(this.links, user.role)
          this.postTypes = Guards.checkLinks(this.postTypes, user.role)
        },
        methods: {
            async logout(){
                const user = this.$store.getters['user/getUser']
                const data = {
                  session: user.session,
                  id: user.id,
                }
                await this.$store.dispatch('user/logout', data)
                const currentUser = this.$store.getters['user/getUser']
                if(!currentUser.login) this.$router.push('/')
            }
        },
    }
</script>

<style scoped>
  .border {
    border: 1px solid red;
  }
  .display_block {
    width:100%;
  }
  .nav-link {
    font-size: 12px;
  }
</style>
