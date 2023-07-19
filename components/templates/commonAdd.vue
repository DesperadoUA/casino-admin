<template>
  <div>
    <v-container>
      <v-row>
        <v-col class="offset-1 col-10 mt-10">
          <h1 class="page_title font-podkova-bold">Add Post</h1>
        </v-col>
      </v-row>
      <v-row>
           <v-col class="mt-0">
                    <MM_Input   v-if = 'data' 
                                :value = 'data.title' 
                                :title = '"Title"'
                                :action = 'action'
                                :action_key = '"title"'
                                 />     
                    <MM_Options v-if = 'data' 
                                :value = 'data.lang' 
                                :all_value = '["ru", "ua"]'
                                :title = '"Lang"'
                                :action = 'action'
                                :action_key = '"lang"'
                                 />
                    <MM_Date    v-if = 'data' 
                                :value = 'data.created_at' 
                                :title = '"Create At"'
                                :action = 'action'
                                :action_key = '"created_at"' />
                    <MM_Date    v-if = 'data' 
                                :value = 'data.updated_at' 
                                :title = '"Update At"'
                                :action = 'action'
                                :action_key = '"updated_at"' />
                    <MM_Image   v-if = 'data' 
                                :value = 'data.path' 
                                :title = '"Video"'
                                :action = 'action'
                                :action_key = '"path"' />
           </v-col>
      </v-row>
    </v-container>
  </div>
</template>
<script>
import MM_Input from '~/components/lib/MM_Input'
import MM_Textarea from '~/components/lib/MM_Textarea'
import MM_Rich_Text from '~/components/lib/MM_Rich_Text'
import MM_Date from '~/components/lib/MM_Date'
import MM_Options from '~/components/lib/MM_Options'
import MM_Image from '~/components/lib/MM_Image'
import MM_Media_Library from '~/components/lib/MM_Media_Library'
    export default {
        name: "commonAdd",
        props: ['data', 'action'],
        components:{MM_Input, MM_Textarea, MM_Rich_Text, MM_Date, MM_Options, MM_Image, MM_Media_Library},
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