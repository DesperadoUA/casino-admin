<template>
    <v-container>
        <v-row>
            <v-col class="mt-0">
                 <MM_Checkbox 
                    :value = 'data.close'
                    :action = 'action' 
                    :title = '"Close"' 
                    :action_key = '"close"'
                />
                <MM_Multiple_Input
                    :value = 'data.ref'
                    :action = 'action' 
                    :title = '"Referal link"' 
                    :action_key = '"ref"'
                    />
                <MM_Input
                    :value = 'data.bonus_wager'
                    :action = 'action' 
                    :title = '"Bonus wager"' 
                    :action_key = '"bonus_wager"'
                    />
                <MM_Input
                    :value = 'data.value_bonus'
                    :action = 'action' 
                    :title = '"Value bonus"' 
                    :action_key = '"value_bonus"'
                    />
            </v-col>
        </v-row>
    </v-container>
</template>

<script>
    import MM_Checkbox from '~/components/lib/MM_Checkbox'
    import MM_Multiple_Input from '~/components/lib/MM_Multiple_Input'
    import MM_Input from '~/components/lib/MM_Input'
    export default {
        name: "bonusMeta",
        props: ['data', 'action'],
        components: {MM_Checkbox, MM_Multiple_Input, MM_Input},
        data() {
            return {}
        }
    }
</script> 