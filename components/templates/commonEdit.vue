<template>
  <div>
    <v-container>
      <v-row>
        <v-col class="offset-1 col-10 mt-10">
          <h1 class="page_title font-podkova-bold" v-if='data'>{{current_title}}</h1>
        </v-col>
      </v-row>
      <v-row>
           <v-col class="mt-0">
                    <MM_Input v-if = 'data' 
                                :value = 'data.title' 
                                :title = '"Title"'
                                :action = 'action'
                                :action_key = '"title"'
                                 /> 
                    <MM_Input v-if = 'data' 
                                :value = 'data.file_id' 
                                :title = '"File id"'
                                :action = 'action'
                                :action_key = '"file_id"'
                                :readonly = 'true'
                                 />
                    <MM_Date v-if = 'data' 
                                :value = 'data.created_at.slice(0, 10)' 
                                :title = '"Create At"'
                                :action = 'action'
                                :action_key = '"created_at"' />
                    <MM_Date v-if = 'data' 
                                :value = 'data.updated_at.slice(0, 10)' 
                                :title = '"Update At"'
                                :action = 'action'
                                :action_key = '"updated_at"' />
                    <MM_Image v-if = 'data' 
                                :value = 'data.path' 
                                :title = '"Path"'
                                :action = 'action'
                                :action_key = '"path"' />
           </v-col>
      </v-row>
    </v-container>
  </div>
</template>
<script>
import MM_Input from '~/components/lib/MM_Input'
import MM_Date from '~/components/lib/MM_Date'
import MM_Image from '~/components/lib/MM_Image'
    export default {
        name: "commonEditStaticPage",
        props: ['data', 'action'],
        components:{MM_Input, MM_Date, MM_Image},
        data(){
          return {
            current_title: ''
          }
        },
        mounted(){
          this.current_title = this.data.title
        }
    }
</script>