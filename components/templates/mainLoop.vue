<template>
  <div>
    <v-container class="container--fluid">
      <v-row>
        <v-col class="offset-1 col-10 mt-10">
          <h1 class="page_title font-podkova-bold">Files</h1>
        </v-col>
      </v-row>
    </v-container>
    <v-container class="container--fluid">
      <v-layout row>
      </v-layout>
    </v-container>
  </div>
</template>

<script>
    import Guards from '~/guards'
    export default {
        name: "mainLoop",
        data(){
            return {}
        },
        mounted(){
          const user = this.$store.getters['user/getUser']
          this.cards = Guards.checkLinks(this.cards, user.role)
        }
    }
</script>

<style scoped>

</style>



