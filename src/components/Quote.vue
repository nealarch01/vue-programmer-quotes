<template>
    <div class="quote-container">
        <div style="flex: 1">
            <p>{{ quoteStr }}</p>
        </div>
        <div style="flex: 1">
            <p>By: {{ author }}</p>
        </div>
    </div>
    <button class="generate-btn" @click="fetchQuoteData()">New Quote</button>
</template>

<script lang="ts">
import { defineComponent, ref, onMounted } from "vue";
import axios from "axios";

export default defineComponent({
    setup() {
        const quoteStr = ref<string>("");
        const author = ref<string>("");

        const fetchQuoteData = async () => {
            let response: any = await axios.get("https://programming-quotes-api.herokuapp.com/Quotes/random");
            if (response.data === undefined) {
                quoteStr.value = "Could not generate a quote. Try again later";
                author.value = "";
                return;
            }

            quoteStr.value = response.data["en"];
            author.value = response.data["author"];
        }

        onMounted(async () => {
            await fetchQuoteData();
        });

        return {
            quoteStr,
            author,
            fetchQuoteData
        }
    }
});

</script>

<style scoped>
div.quote-container {
    display: flex;
    flex-direction: column;
    background-color: #0B0014;
    border-radius: 12px;
    padding-right: 20px;
    padding-left: 20px;
    padding-top: 10px;
    padding-bottom: 10px;
    width: 800px;
    min-height: 90px;
}

button.generate-btn {
    height: 50px;
    width: 250px;
    background-color: #3C91E6;
    border: none;
    font-weight: bold;
    color: white;
    align-self: center;
    margin-top: 10px;
    border-radius: 12px;
    font-size: 20px;
}

button.generate-btn:active {
    opacity: 0.6;
}

p {
    color: white;
    margin: 10px;
}
</style>