<template lang="">
    <div class="avatar">
        <img :src="text">
    </div>
</template>

<script>
export default {
    name:'AppAvatar',
    data() {
        return {
            text: this.$attrs.text
        }
    },
    
}

</script>
<style lang="">
    
</style>