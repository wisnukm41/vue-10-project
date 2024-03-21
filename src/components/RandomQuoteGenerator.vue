<template>
    <div class="quote-generator">
        <h1 class="app-title">Random Quote Gens</h1>
        <blockquote class="quote-container">
            <p>{{ currentQuote.text }}</p>
            <cite>{{ currentQuote.author }}</cite>
        </blockquote>

        <button @click="getRandomQuotes" class="quote-button">Get Random Quote</button>
    </div>
</template>

<script setup>
    import { onMounted, ref } from 'vue';

    const quotes = ref([{
                text : 'Happiness is like a butterfly: the more you chase it, the more it will evade you, but if you notice the other things around you, it will gently come and sit on your shoulder.',
                author : 'Henry David Thoreau'
            },{
                text : 'Hard choices, easy life. Easy choices, hard life.',
                author : 'Jerzy Gregorek'
            },{
                text : 'You will never change your life until you change something you do daily.',
                author : 'John Maxwell'
            }
        ]);
    
    const currentQuote = ref({text:'', author:''});

    const getRandomQuotes = () => {
        const randomIndex = Math.floor(Math.random() * quotes.value.length)
        currentQuote.value = quotes.value[randomIndex];
    }

    onMounted(getRandomQuotes)
</script>

<style scoped>
    .quote-generator {
    max-width: 400px;
    margin: 50px auto;
    padding: 20px;
    text-align: center;
    border: 1px solid #ccc;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    }

    .app-title {
    font-size: 24px;
    margin-bottom: 20px;
    color: #333;
    }

    .quote-container {
    background-color: #f9f9f9;
    padding: 20px;
    border-radius: 8px;
    border: 1px solid #ddd;
    margin-bottom: 20px;
    }

    p {
    font-size: 18px;
    margin-bottom: 10px;
    }

    cite {
    font-style: normal;
    color: #777;
    }

    .quote-button {
    padding: 10px 20px;
    font-size: 16px;
    background-color: #3498db;
    color: #fff;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    }

    .quote-button:hover {
    background-color: #2980b9;
    }
</style>