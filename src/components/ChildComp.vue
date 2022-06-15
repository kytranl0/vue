<script>
export default {
    props: {
        msg: String
    }
}
</script>
<template>
    <h1>{{msg || 'No props passed yet'}}</h1>
</template>