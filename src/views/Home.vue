<template>
    <div class="home-container">
        <div class="home-container__header">
            <top-header />
        </div>
        <div class="home-container__map">
            <cesium-viewer @getViewer="getViewer"/>
        </div>
    </div>
</template>

<script>
    import TopHeader from '@/views/header/top-header'
    export default {
        components: {
            TopHeader
        },
        methods: {
            getViewer(viewer) {
                window.viewer = viewer
            }
        }
    }
</script>

<style lang='scss' scoped>
    .home-container {
        width: 100%;
        height: 100%;

        &__header {
            width: 100%;
            position: absolute;
            top: 0;
            left: 0;
            z-index: 999;
        }

        &__map {
            width: 100%;
            height: 100%;
            position: absolute;
            top: 0;
            left: 0;
            z-index: 1;
        }
    }
</style>
