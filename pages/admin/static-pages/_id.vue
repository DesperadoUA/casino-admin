<template>
  <div>
    <commonEditStaticPage v-if='data.body' 
                     :data = "data.body"
                     :action = '"static_pages/changeStateCurrentPage"'>
    </commonEditStaticPage>
    <v-container>
        <v-row>
          <v-col class="offset-1 col-10 mt-5 mb-10">
            <v-btn
                  class="font-podkova-bold deep-orange darken-2"
                  text
                  @click="update()"
          >
            Update
          </v-btn>
          </v-col>
        </v-row>
    </v-container>
    <snackeBar :status = "snackbar.status"
               :text = "snackbar.text"
               :timeout = "snackbar.timeout"
    />
  </div>
</template>

<script>
import commonEditStaticPage from '~/components/templates/commonEditStaticPage'
import snackeBar from '~/components/templates/snackbar'
import Guards from '~/guards'
    export default {
        name: "singleStaticPage",
        layout: 'admin',
        components: {commonEditStaticPage, snackeBar},
        async mounted() {
            const user = this.$store.getters['user/getUser']
            if(!Guards.checkRouts(this.guard, user.role)) this.$router.replace('/admin')
            const data = {
                session: user.session,
                id: user.id,
                url: this.$route.params.id
            }
            await this.$store.dispatch('static_pages/setCurrentPage', data)
            this.data.body = this.$store.getters['static_pages/getCurrentPage']
        },
        data(){
          return {
              data:{
                body: undefined,
              },
              snackbar: {
                  status: false,
                  text: 'Post Update',
                  timeout: 5000
                },
              guard: 'page'
          }
        },
        methods: {
          async update(){
            const user = this.$store.getters['user/getUser']
            const data = {
                session: user.session,
                id: user.id,
                data: this.$store.getters['static_pages/getCurrentPage']
            }
            await this.$store.dispatch('static_pages/updateCurrentPage', data)
            this.snackbar.status = true
            setTimeout(()=>{
              this.snackbar.status = false  
            }, this.snackbar.timeout)
          }
        }
    }
</script>

<style scoped>

</style>