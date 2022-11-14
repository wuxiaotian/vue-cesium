<template>
    <div id="cesium-container">
        <slot/>
    </div>
</template>

<script>

    export default {
        mounted() {
            this.initViewer()
        },
        props: {
            extent: {
                type: Array,
                default: () => {
                    return [
                        48.22696647618958,
                        2.1125147967573135,
                        167.42693968753903,
                        56.55421267639345
                    ]
                }
            }
        },
        methods: {
            initViewer() {
                Cesium.Ion.defaultAccessToken = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiIwM2ZkNjljMi1hOWExLTQ1MjAtOTRhOS02ZjJlZjc2NzdlZmUiLCJpZCI6MzI0MjQsInNjb3BlcyI6WyJhc3IiLCJnYyJdLCJpYXQiOjE1OTY5ODQ1OTV9.jkeMqWfeanzrHgMmsbrIsN-UcoA4CxVCP8euZeBXL9Y';
                const viewer = new Cesium.Viewer('cesium-container', {
                    navigationHelpButton: false,
                    vrButton: false,
                    baseLayerPicker: false,
                    animation: false,
                    fullscreenButton: false,
                    timeline: false,
                    geocoder: false,
                    scene3DOnly: true,
                    homeButton: false,
                    infoBox: false,
                    selectionIndicator: false,
                    contextOptions: {
                        id: "cesiumCanvas",
                        webgl: {
                            alpha: true,
                            depth: true,
                            stencil: true,
                            antialias: true,
                            premultipliedAlpha: true,
                            //通过canvas.toDataURL()实现截图需要将该项设置为true
                            preserveDrawingBuffer: true,
                            failIfMajorPerformanceCaveat: true
                        }
                    }
                })
                viewer.scene.globe.depthTestAgainstTerrain = true
                viewer._cesiumWidget._creditContainer.style.display = 'none'

                this.fullScreen(viewer, this.extent)

                this.$emit('getViewer', viewer)
            },
            fullScreen(viewer, extent) {
                viewer.camera.flyTo({
                    destination: Cesium.Rectangle.fromDegrees(
                        extent[0],
                        extent[1],
                        extent[2],
                        extent[3]),
                    duration: 2
                })
            }
        }
    }
</script>

<style scoped lang="scss">
    #cesium-container {
        height: 100%;
        width: 100%;
    }
</style>
