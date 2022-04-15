<template>
    <v-container>
        <v-row>
            <v-col class="mt-0">
                <MM_Input
                    :value = 'data.iframe'
                    :action = 'action' 
                    :title = '"iframe"' 
                    :action_key = '"iframe"'
                />
                <MM_Rating 
                    :value = 'data.rating'
                    :action = 'action' 
                    :title = '"Rating"' 
                    :action_key = '"rating"'
                />
                <MM_Input
                    :value = 'data.number_games'
                    :action = 'action' 
                    :title = '"Number games"' 
                    :action_key = '"number_games"'
                />
                <MM_Multiple_Two_Input
                    :value = 'data.details'
                    :action = 'action' 
                    :title = '"Details"' 
                    :action_key = '"details"'
                /> 
                <MM_Characters_Game 
                    :value = 'data.characters'
                    :action = 'action' 
                    :title = '"Characters"' 
                    :action_key = '"characters"' 
                />
                <MM_Multiple_Two_Input_Image 
                    :value = 'data.galery'
                    :action = 'action' 
                    :title = '"Galery"' 
                    :action_key = '"galery"' 
                />
            </v-col>
        </v-row>
    </v-container>
</template>

<script>
    import MM_Multiple_Input_Text from '~/components/lib/MM_Multiple_Input_Text'
    import MM_Input from '~/components/lib/MM_Input'
    import MM_Multiple_Input from '~/components/lib/MM_Multiple_Input'
    import MM_Checkbox from '~/components/lib/MM_Checkbox'
    import MM_Characters_Game from '~/components/lib/MM_Characters_Game'    
    import MM_Multiple_Two_Input_Image from '~/components/lib/MM_Multiple_Two_Input_Image' 
    import MM_Rating from '~/components/lib/MM_Rating' 
    export default {
        name: "slotMeta",
        props: ['data', 'action'],
        components: {MM_Multiple_Input_Text, MM_Input, MM_Multiple_Input, MM_Checkbox, MM_Characters_Game, 
        MM_Multiple_Two_Input_Image, MM_Rating},
        data() {
            return {}
        }
    }
</script>