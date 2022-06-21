<script>
export default {
    props: {
        msg: String
    },
    emits: ['response'],
    created() {
        this.$emit('response', 'hello from child')
    }
}
</script>
<template>
    <h1>{{msg || 'No props passed yet'}}</h1>
</template>