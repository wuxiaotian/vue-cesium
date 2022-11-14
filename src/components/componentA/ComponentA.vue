<template>
    <div>组件A {{text}}</div>
</template>

<script>
    import {mapState} from "vuex";

    export default {
        name: "ComponentA",
        computed: {
            ...mapState({
                text: (state) => state.data.text
            })
        }

    }
</script>

<style scoped>

</style>