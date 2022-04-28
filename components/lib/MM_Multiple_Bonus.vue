<template>
  <v-container class="container--fluid pa-0">
    <v-row>
      <v-col class="offset-1 col-10 font-podkova-bold blue-grey darken-4">
        <v-expansion-panels inset>
          <v-expansion-panel>
            <v-expansion-panel-header >{{title}}</v-expansion-panel-header>
            <v-expansion-panel-content class="pt-4">
              <v-container class="bb_orange" v-for="(item, index) in currentData" :key = "index">
              <v-row class="pa-2 mb-2 slider_item_wrapper">
                <div class="col-lg-3 col-xs-12">
                  <img :src="currentData[index].src"
                       class="mm_image margin_bottom_15"
                  >
                </div>
                <div class="col-lg-3 col-xs-12">
                  <input type="file"
                         :id="'file_'+action_key+'_'+index"
                         class="mm_input margin_bottom_15 inputFile"
                         :ref="action_key"
                         @change="selectFile(index)"
                  > <label :for="'file_'+action_key+'_'+index" class="mt-7">Choose a file ...</label>
                </div>
                <div class="col-lg-6 col-xs-12">
                  <v-text-field 
                        prepend-icon = "mdi-tooltip-edit"
                        type = "text"
                        color = "deep-orange darken-2"
                        v-model = "currentData[index].value_1"
                        @change = "change" 
                  ></v-text-field>
                  <v-text-field 
                        prepend-icon = "mdi-tooltip-edit"
                        type = "text"
                        color = "deep-orange darken-2"
                        v-model = "currentData[index].value_2"
                        @change = "change"
                    ></v-text-field>
                  <v-text-field 
                        prepend-icon = "mdi-tooltip-edit"
                        type = "text"
                        color = "deep-orange darken-2"
                        v-model = "currentData[index].value_3"
                        @change = "change"
                    ></v-text-field>
                  <v-text-field 
                        prepend-icon = "mdi-tooltip-edit"
                        type = "text"
                        color = "deep-orange darken-2"
                        v-model = "currentData[index].value_4"
                        @change = "change"
                    ></v-text-field>
                    <v-text-field 
                        prepend-icon = "mdi-tooltip-edit"
                        type = "text"
                        color = "deep-orange darken-2"
                        v-model = "currentData[index].value_5"
                        @change = "change"
                    ></v-text-field>
                  <v-btn
                      class="deep-orange darken-2 font-podkova-bold mt-5"
                      @click="deleteItem(item)"
                  >
                  <v-icon left>mdi-delete</v-icon>
                  Delete
                  </v-btn>
                </div>
              </v-row>
              </v-container>
              <v-btn
                      class="deep-orange darken-2 font-podkova-bold mt-5"
                      @click="addItem"
              >
                <v-icon left>mdi-playlist-plus</v-icon>
                Add
              </v-btn>
            </v-expansion-panel-content>
          </v-expansion-panel>
        </v-expansion-panels>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
    import axios from 'axios'
    import config from '~/DAL/config'
    export default {
        name: "MM_Multiple_Two_Input_Image",
        props: ['value', 'title', 'action', 'action_key'],
        data(){
            return {
                currentData: []
            }
        },
        methods: {
            addItem(){
              this.currentData.push({
                src: '',
                value_1: '',
                value_2: '',
                value_3: '',
                value_4: '',
                value_5: ''
              })
              const currentData = {
                      key: this.action_key,
                      value: this.currentData
                    }
              this.$store.dispatch(this.action, currentData)
            },
            change(){
              const currentData = {
                      key: this.action_key,
                      value: this.currentData
                    }
              this.$store.dispatch(this.action, currentData)
            },
            async selectFile(index){
              console.log(this.action_key)
              const file = this.$refs[this.action_key][index].files[0]
              if(file) {
                  const reader = new FileReader();
                  reader.onloadend = async () => {
                    const user = this.$store.getters['user/getUser']
                    const data = {
                        session: user.session,
                        id: user.id,
                        file: {
                          name: file.name,
                          base64: reader.result
                        }
                    }
                    const result = await axios.post(config.API_URL+'uploads', data)
                    this.currentData[index].src = result.data.src
                    const currentData = {
                      key: this.action_key,
                      value: this.currentData
                    }
                    this.$store.dispatch(this.action, currentData)    
                  }
                  reader.readAsDataURL(file);
              }
            },
            deleteItem(item){
              this.currentData = this.currentData.filter(obj => obj !== item)
              const currentData = {
                      key: this.action_key,
                      value: this.currentData
                    }
              this.$store.dispatch(this.action, currentData) 
            },
        },
        mounted(){
          this.currentData = this.value
        }
    }
</script>

<style scoped>

</style>