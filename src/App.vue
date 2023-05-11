<template>
  <div>
    <p>Last Barcode: {{ lastBarcode }}</p>
    <button @click="evento">CLick event</button>
    <input style="border: 1px solid #000;">
  </div>
</template>

<script lang="ts" setup>
import { ref, onMounted } from 'vue';
let barcode = ref("");
let interval: ReturnType<typeof setTimeout>;
let lastBarcode = ref('')

const handler = (evt: KeyboardEvent) => {
  lastBarcode.value = ""
  window.focus()
  if (interval) clearInterval(interval);
  if (evt.code === "Enter") {
    if (barcode.value) {

        lastBarcode.value = barcode.value

      return;
    }
  }
  if (evt.key !== "Shift") barcode.value += evt.key;
  interval = setInterval(() => (barcode.value = ""), 200000);
};

const evento = ()=>{
  console.log("Hola Mundo")
}

onMounted(() => {
  window.addEventListener("keydown", handler);
})
</script>
