<script setup lang="ts">
import HelloWorld from './components/HelloWorld.vue'

import { configureEcho } from "@laravel/echo-vue";
import { useEcho } from "@laravel/echo-vue";
 

configureEcho({
    broadcaster: "pusher",
    key: import.meta.env.VITE_PUSHER_APP_KEY,
    cluster: import.meta.env.VITE_PUSHER_APP_CLUSTER,
    forceTLS: true,
    authEndpoint: import.meta.env.VITE_PUSHER_AUTH_ENDPOINT,
    bearerToken: import.meta.env.VITE_TEMP_TOKEN // idealmente deberia ser un token de usuario logueado, pero para el ejemplo lo pongo fijo
});


let orderId = 1;

useEcho(
    `orders.${orderId}`,
    "OrderShipmentStatusUpdated",
    (e) => {
        console.log(e.order);
    },
);

</script>

<template>
  <HelloWorld />
</template>
