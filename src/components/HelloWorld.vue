<script setup>
defineProps({
  msg: {
    type: String,
    required: true,
  },
});
</script>
<script>
import { generateOnRampURL } from "@coinbase/cbpay-js";
export default {
  data() {
    return { isReady: false, url: "" };
  },
  created() {
    console.log(this.isReady);
  },
  mounted() {
    console.log("mounted");
    this.isReady = true;
    this.url = generateOnRampURL({
      appId: "your_app_id",
      destinationWallets: [
        {
          address: "0x016...",
          blockchains: ["ethereum"],
          // or by individual asset
          //assets: ["ETH", "USDC", "DAI"]
        },
      ],
    });
    console.log(this.url);
  },
  methods: {
    open() {
      if (this.url.length > 0) {
        window.open(this.url);
      }
    },
  },
};
</script>
<template>
  <div class="greetings">
    <h1 class="green">{{ msg }}</h1>
    <h2>Initialized? {{ isReady }}</h2>
    <button @click="open">Buy Now</button>
    <h3>
      You’ve successfully created a project with
      <a href="https://vitejs.dev/" target="_blank" rel="noopener">Vite</a> +
      <a href="https://vuejs.org/" target="_blank" rel="noopener">Vue 3</a>.
    </h3>
  </div>
</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>
