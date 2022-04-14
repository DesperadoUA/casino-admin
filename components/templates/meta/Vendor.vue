<template>
    <v-container>
        <v-row>
            <v-col class="mt-0">
                <MM_Input
                    :value = 'data.year'
                    :action = 'action' 
                    :title = '"Year"' 
                    :action_key = '"year"'
                    />
                <MM_Input
                    :value = 'data.number_games'
                    :action = 'action' 
                    :title = '"Number games"' 
                    :action_key = '"number_games"'
                    />
            </v-col>
        </v-row>
    </v-container>
</template>

<script>
    import MM_Input from '~/components/lib/MM_Input'
    export default {
        name: "licenseMeta",
        props: ['data', 'action'],
        components: {MM_Input},
        data() {
            return {}
        }
    }
</script> 