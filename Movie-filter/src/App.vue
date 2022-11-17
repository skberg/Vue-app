<script setup>
import FetchComp from "./components/Fetch.vue"

components: {
    FetchComp
}
</script>

<template>
    <h1><span class="HedingStart">Movies</span></h1>
    <div class="holder">
        <div class="wave"></div>
        <div class="wave"></div>
        <div class="wave"></div>
        <FetchComp></FetchComp>
    </div>
</template>

<style scoped>
.holder {
    max-width: max-content;
    margin: auto;
    min-width: 500px;
}

h1 {
    margin: 15px;
    font-size: 3rem;
    font-family: Arial, Helvetica, sans-serif;
    font-weight: 900;
    color: rgba(235, 235, 235, 0.64);
}

.HedingStart {
    background: linear-gradient(-45deg, #609d9f, #609d9f, #e89a3e, #e89a3e);
    background-size: 300%;
    font-family: Arial, Helvetica, sans-serif;
    font-weight: 900;
    letter-spacing: -2px;
    text-transform: uppercase;
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    animation: animated_text 10s ease-in-out infinite;
    -moz-animation: animated_text 10s ease-in-out infinite;
    -webkit-animation: animated_text 10s ease-in-out infinite;
}

@keyframes animated_text {
    0% {
        background-position: 0px 50%;
    }
    50% {
        background-position: 100% 50%;
    }
    100% {
        background-position: 0px 50%;
    }
}

.wave {
    background: rgba(90, 143, 163, 0.357);
    border-radius: 1000% 1000% 0 0;
    position: fixed;
    width: 200%;
    height: 12em;
    animation: wave 10s -3s linear infinite;
    transform: translate3d(0, 0, 0);
    opacity: 0.5;
    bottom: 0;
    left: 0;
    z-index: -1;
}

.wave:nth-of-type(2) {
    bottom: -1.25em;
    animation: wave 18s linear reverse infinite;
    opacity: 0.8;
}

.wave:nth-of-type(3) {
    bottom: -2.5em;
    animation: wave 20s -1s reverse infinite;
    opacity: 0.9;
}

@keyframes wave {
    2% {
        transform: translateX(1);
    }
    25% {
        transform: translateX(-25%);
    }
    50% {
        transform: translateX(-50%);
    }
    75% {
        transform: translateX(-25%);
    }
    100% {
        transform: translateX(1);
    }
}
</style>
