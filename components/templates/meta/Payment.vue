<template>
    <v-container>
        <v-row>
            <v-col class="mt-0">
                <MM_Input
                    :value = 'data.site'
                    :action = 'action' 
                    :title = '"Site"' 
                    :action_key = '"site"'
                    />
                <MM_Input
                    :value = 'data.withdrawal'
                    :action = 'action' 
                    :title = '"Withdrawal"' 
                    :action_key = '"withdrawal"'
                    />
                <MM_Input
                    :value = 'data.commission'
                    :action = 'action' 
                    :title = '"Commission"' 
                    :action_key = '"commission"'
                    />
                <MM_Input
                    :value = 'data.withdrawal_period'
                    :action = 'action' 
                    :title = '"Withdrawal period"' 
                    :action_key = '"withdrawal_period"'
                    />
            </v-col>
        </v-row>
    </v-container>
</template>

<script>
    import MM_Multiple_Input_Text from '~/components/lib/MM_Multiple_Input_Text'
    import MM_Input from '~/components/lib/MM_Input'
    export default {
        name: "paymentMeta",
        props: ['data', 'action'],
        components: {MM_Multiple_Input_Text, MM_Input},
        data() {
            return {}
        }
    }
</script> 