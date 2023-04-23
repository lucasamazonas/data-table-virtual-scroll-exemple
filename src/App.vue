<script setup lang="ts">
import LDataTable from "@/components/LDataTable/Index.vue"

const headers = [
    { text: "Cabecallho 01", value: "valor" },
    { text: "Cabecallho 02", value: "valor" },
    { text: "Cabecallho 03", value: "valor" },
    { text: "Cabecallho 04", value: "valor" },
    { text: "Cabecallho 05", value: "valor" },
    { text: "Cabecallho 06", value: "valor" },
]

const items = Array(5000).fill(0).map((_, index) => ({
    valor: index
}))
</script>

<template>
  <LDataTable
    :headers="headers"
    :items="items"
    :height="180"
    :heightItem="30"
  />
</template>

<style scoped>

</style>
