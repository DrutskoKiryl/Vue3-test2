<template lang="">
   <h2>{{ text }}</h2>
</template>

<script>
export default {
    name: 'AppSubtitle',
    data() {
        return {
            text: this.$attrs.text
        }
    },
    
}

</script>
<style lang="">
    
</style>