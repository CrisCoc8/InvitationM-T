<template>
    <section v-if="time > 0" style="width: 100%; margin-bottom: 7.5vh">
        <vue-countdown v-if="time > 0" :time="time" v-slot="{ days = 0, hours = 0, minutes = 0, seconds = 0 }" style="width: 100%;">
       <section class="countdown-section">
            <article class="countdown-article">
                <div class="number"> {{ days }}</div>
                <div class="time-unit">día{{ days > 1 ? 's' : '' }} </div>
            </article>
            <article class="countdown-article">
                <div class="number"> {{ hours }}</div>
                <div class="time-unit">hora{{ hours > 1 ? 's' : '' }}</div>
            </article>
            <article class="countdown-article">
                <div class="number"> {{ minutes }}</div>
                <div class="time-unit">minuto{{ minutes > 1 ? 's' : '' }}</div>
            </article>
            <article class="countdown-article">
                <div class="number"> {{ seconds }}</div>
                <div class="time-unit">segundo{{ seconds == 1 ? '' : 's' }}</div>
            </article>
       </section>
    </vue-countdown>
    </section>
    <section v-else style="width: 100%; margin-bottom: 7.5vh">
        <h1 class="occurring-message">Está ocurriendo, ¡Disfruta!</h1>
    </section>
</template>
<script setup>
    import { ref, onMounted } from 'vue';
    //26 de noviembre de 2024 a las 5 PM (meses inician desde 0)
    const targetDate = new Date(2024, 9, 26, 17, 0, 0);
    //const targetDate = new Date(2024, 8, 11, 2, 5, 0);
    const time = ref(0);

    onMounted(() => {
        const now = new Date();
        const timeDifference = targetDate.getTime() - now.getTime();
        
        time.value = Math.max(timeDifference, 0);

        const updateCountdown = setInterval(() => {
            const now = new Date();
            time.value = Math.max(targetDate.getTime() - now.getTime(), 0);

            if (time.value <= 0) {
            clearInterval(updateCountdown);
            }
        }, 1000);
    });
</script>
<style scoped>
    .countdown-section{
        display: flex;
        justify-content: space-around;
        width: 85%;
        flex-wrap: wrap;
        margin: 0 7.5%;
    }
    .countdown-article{
        display: flex;
        flex-direction: column;
        justify-content: center;
        gap: 15px;
        align-items: center;
        width: 22.5%;
    }
    .number{
        font-style: italic;
        color:  white;
        @apply text-2xl md:text-4xl lg:text-5xl;
        font-weight: 700;
        text-shadow: 1px 1px 6px rgba(0,0,0,0.9), 4px 4px 6px rgba(0,0,0,0.5), 8px 8px 11px rgba(0,0,0,0.75), 22px 22px 20px rgba(0,0,0,0.4), -2px -2px 5px rgba(0,0,0,0.2), 2px 2px 5px rgba(0,0,0,0.2) !important;
    }
    .time-unit{
        text-transform: none;
        color:  white;
        @apply text-base md:text-xl lg:text-2xl;
        font-weight: 500;
        font-style: italic;
        text-shadow: 1px 1px 6px rgba(0,0,0,0.9), 4px 4px 6px rgba(0,0,0,0.5), 8px 8px 11px rgba(0,0,0,0.75), 22px 22px 20px rgba(0,0,0,0.4), -2px -2px 5px rgba(0,0,0,0.2), 2px 2px 5px rgba(0,0,0,0.2) !important;
    }

    .occurring-message{
        font-family: Montserrat;
        font-weight: 400;
        text-shadow: 1px 1px 6px rgba(0,0,0,0.9), 4px 4px 6px rgba(0,0,0,0.5), 8px 8px 11px rgba(0,0,0,0.75), 22px 22px 20px rgba(0,0,0,0.4), -2px -2px 5px rgba(0,0,0,0.2), 2px 2px 5px rgba(0,0,0,0.2) !important;
        color: white;
        @apply text-3xl md:text-5xl;
        font-style: italic;
        text-align: center;
    }
</style>