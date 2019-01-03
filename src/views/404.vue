<template>
    <div class="nofind">
        <!--<img src="../assets/404.gif" alt="">-->
        <div class="mc-panel">
            <MerryChristmas></MerryChristmas>
        </div>
        <!--<Fireworks></Fireworks>-->
    </div>
</template>
<script>
    import MerryChristmas from '../components/MerryChristmas'
    import Fireworks from '../components/Fireworks'

    export default {
        name: '404',
        data() {
            return {};
        },
        components: {MerryChristmas, Fireworks}
    }
</script>
<style scoped>
    .nofind {
        width: 100%;
        height: 100%;
        overflow: hidden;
        position: relative;
    }

    .nofind img {
        width: 100%;
        height: 100%;
    }

    .mc-panel {
        position: absolute;
        height:580px;
        width:1200px;
        top: 0;
        bottom: 0;
        left: 0;
        right: 0;
        margin:auto;
        background-image: url("../assets/bg1.jpg");
        background-repeat: no-repeat;
    }

    .mc-msg {
        float:left;
        display: inline-block;
    }
</style>

