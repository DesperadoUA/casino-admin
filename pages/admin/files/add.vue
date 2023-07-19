<template>
  <div>
   <commonAdd   v-if = 'data.body' 
                :data = "data.body"
                :action = 'STORE_DIR + "/changeStateNewPost"'></commonAdd>
    <v-container>
        <v-row>
          <v-col class="offset-1 col-10 mt-5 mb-10">
            <v-btn
                  class="font-podkova-bold deep-orange darken-2"
                  text
                  @click="add()"
          >
           <v-icon left color="white">mdi-folder-plus</v-icon>
            Add
          </v-btn>
          </v-col>
        </v-row>
    </v-container>
  </div>
</template>

<script>
import commonAdd from '~/components/templates/commonAdd.vue'
import Guards from '~/guards'
    export default {
        name: "fileAdd", 
        layout: 'admin',
        components: {commonAdd},
        mounted() {   
          const user = this.$store.getters['user/getUser']
          if(!Guards.checkRouts(this.guard, user.role)) this.$router.replace('/')
          this.data.body = {
               title:  '',
               lang: 'ru',
               path: '',
               updated_at: new Date().toJSON().slice(0,10),
               created_at: new Date().toJSON().slice(0,10)
           }
           this.$store.dispatch(this.STORE_DIR + '/setNewPost', this.data.body)
        },
        data(){
          return {
              data:{
                body: undefined
              },
              STORE_DIR: 'files/post',
              guard: 'file',
              slug: 'files'
          }
        },
        methods: {
          async add(){
            const user = this.$store.getters['user/getUser']
            const data = {
                session: user.session,
                id: user.id,
                data: this.$store.getters[this.STORE_DIR + '/getNewPost']
            }
            if(data.data.title !== '' && data.data.path !== '') {
                await this.$store.dispatch(this.STORE_DIR + '/addNewPost', data)
                const insertId = this.$store.getters[this.STORE_DIR + '/getInsertId']
                if(insertId !== '') this.$router.push(`/admin/${this.slug}/${insertId}`)
            } 
            else {
                alert('Title or path empty')
            }
          }
        }
    }
</script>

<style scoped>

</style>