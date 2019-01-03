<template>
    <div class="letter-panel">
        <div class="letter-merry">
            <MerryChristmas></MerryChristmas>
        </div>
        <div class="letter-msg">
            世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！世界，你好！
        </div>
    </div>
</template>

<script>
    import MerryChristmas from '../components/MerryChristmas'

    export default {
        name: 'letter',
        data() {
        },
        components:{MerryChristmas},
        created() {
        },
        mounted() {
        },
        methods: {}
    }
</script>

<style scoped>
    .letter-panel {
        height:100%;
        position:relative;
        margin: 0 10%;
        padding: 0;
        overflow: hidden;
    }

    .letter-merry {
        height:50%;
        width:30%;
        margin:14% 0;
        float:left;
    }

    .letter-msg{
        height:50%;
        width:70%;
        margin:14% 0;
        float:left;
        background: #4db3ff;
        text-decoration: underline;
        line-height: 32px;
        display: inline-block;
    }
</style>