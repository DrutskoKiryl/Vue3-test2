<template lang="">
    <h1>{{ text }}</h1>
</template>

<script>
export default {
    name: 'AppTitle',
    data() {
        return {
            text: this.$attrs.text
        }
    },
}
</script>

<style lang="">
    
</style>