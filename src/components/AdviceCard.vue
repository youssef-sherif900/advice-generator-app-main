<template>
    <div class="body">
        <div class="container">
            <p class="title"> ADVICE #{{ id }}</p>
            <h1 class="advice">{{ advice }}</h1>
            <div class="divdor"></div>
            <button class="btn" @click="fetchData">
                <img src="../assets/icon-dice.svg" alt="dice" class="dice">
            </button>
        </div>
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

import axios from 'axios'

const id = ref(0)
const advice = ref('')

const fetchData = async () => {
  const { data: { slip } } = await axios.get('https://api.adviceslip.com/advice')
  id.value = slip.id
  advice.value = slip.advice
}

onMounted(fetchData)
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Kumbh+Sans:wght@700&family=Manrope:wght@800&display=swap');

.body {
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: hsl(217, 19%, 24%);
}

.container {
    position: relative;
    width: 30vw;
    aspect-ratio: 1.5/1;
    border-radius: 1.5rem;
    background-color: hsl(218, 23%, 16%);
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    font-family: 'Kumbh Sans', sans-serif;
    font-family: 'Manrope', sans-serif;
    padding: 1.5rem;
}

.title {
    letter-spacing: 5px;
    color: hsl(150, 100%, 66%);
}

.advice {
    text-align: center;
    color: hsl(193, 38%, 86%);
}

.divdor {
    background-image: url("../assets/pattern-divider-desktop.svg");
    background-repeat: no-repeat;
    background-size: contain;
    width: 90%;
    height: 10%;
    margin-top: 1rem;
}

.btn {
    position: absolute;
    bottom: 0%;
    transform: translateY(50%);
    width: 4rem;
    height: 4rem;
    border: none;
    border-radius: 100%;
    background-color: hsl(150, 100%, 66%);
}

.btn:hover {
    cursor: pointer;
    box-shadow: 0 0 10px hsl(150, 100%, 66%), 0 0 40px hsl(150, 100%, 66%), 0 0 80px hsl(150, 100%, 66%);

}

@media screen and (max-width: 750px) {
    .title {
        font-size: medium;
    }

    .advice {
        font-size: large;
    }

    .divdor {
        background-image: url("../assets/pattern-divider-mobile.svg");
    }

    .btn {
        width: 3rem;
        height: 3rem;
    }
    .container{
        width: 60vw;
    }
}</style>
