<template>
    <b-btn v-on:click="buttonClicked" :variant="btnType">{{text}}</b-btn>
</template>

<script>

export default {
    name: 'Button',
    props: {
        text: String,
        btnType: String,
    },
    methods: {
        buttonClicked: function () {
            this.$emit('click:option')
        }
    }
    
}
</script>
