<script setup lang="ts">
import {computed, ref} from "vue";

interface ItemHeader {
    text: string,
    value: string,
}

interface Props {
    headers: ItemHeader[],
    items: Object[],
    height: number,
    heightItem: number,
    extrasItems: number,
    fixedHeader: boolean,
}

const props = withDefaults(defineProps<Props>(), {
    heightItem: 45,
    extrasItems: 0,
    fixedHeader: false,
})

const firstItem = ref(0)

const styleContentComputed = computed(() => ({
  height: `${props.height}px`,
}))

const styleRowComputed = computed(() => ({
  height: `${props.heightItem}px`,
}))

const quantityItemsRender = computed(() => Math.ceil(props.height / props.heightItem) + props.extrasItems);

const itemsRender = computed(() => {
  return props.items.slice(firstItem.value, firstItem.value + quantityItemsRender.value)
})

const scrollHeigthBottom = computed(() => {
  const heightBeforeBottom = (firstItem.value + quantityItemsRender.value) * props.heightItem
  return Math.max((props.items.length * props.heightItem) - heightBeforeBottom, 0);
})

function scrollY(ev: any) {
  firstItem.value = Math.trunc(ev.target.scrollTop / props.heightItem)
}
</script>

<template>
  <div class="content" :style="styleContentComputed" @scroll="scrollY">
    <div :style="{ marginBottom: `${scrollHeigthBottom}px` }">
      <table class="fixed-header">
        <thead>
          <tr>
            <th v-for="(header, indexColumn) in props.headers" :key="indexColumn">
              {{ header.text }}
            </th>
          </tr>
        </thead>

        <tbody>
          <tr>
            <td :style="{ paddingTop: `${firstItem * props.heightItem}px` }" :colspan="headers.length" />
          </tr>

          <tr v-for="(item, indexRow) in itemsRender" :key="indexRow" :style="styleRowComputed">
            <td v-for="(header, indexColumn) in props.headers" :key="indexColumn">
              {{ item[header.value] }}
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<style scoped>
.content {
  overflow: auto;
}
.content table {
  width: 100%;
  font-size: 12px;
  border-collapse: collapse;
}
.content table tr th {
  text-align: left;
}
.content table tr td {
  border-bottom: 1px solid #d7d7d7;
}
.fixed-header thead tr th {
  position: sticky;
  top: 0;
}
</style>
