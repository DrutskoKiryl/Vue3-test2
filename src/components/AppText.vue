<template lang="">
    <p>{{ text }}</p>
</template>

<script>
export default {
    name: 'AppText',
    data() {
        return {
           text: this.$attrs.text 
        }
    },
}
</script>

<style lang="">
    
</style>