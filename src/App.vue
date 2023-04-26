<script setup lang="ts">
import LDataTable from "@/components/LDataTable/Index.vue"

const headers = [
    { text: "Descrição do Produto", value: "descricao" },
    { text: "Preço médio de custo", value: "preco" },
    { text: "Valor médio de venda", value: "valor" },
    { text: "Saldo de estoque", value: "estoque" },
]

const items = Array(50).fill(0).map((_, index) => ({
    descricao: "Lucas Amazonas " + index + ' KG',
    preco: 12.3,
    valor: index,
    estoque: index * 0.2
}))
</script>

<template>
  <LDataTable
    style="margin: 100px 20px"
    :headers="headers"
    :items="items"
    :height="400"
    fixed-header
  />
</template>

<style scoped>

</style>
