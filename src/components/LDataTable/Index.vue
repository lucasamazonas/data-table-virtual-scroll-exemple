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
}

const countItemRender = 6

const props = defineProps<Props>()

const scrollHeightTop = ref(0)

const styleContentComputed = computed(() => ({
    height: `${props.height}px`,
}))

// const styleRowComputed = computed(() => ({
//     height: `${props.heightItem}px !important`,
// }))
//
// const itemsRender = computed(() => {
//     const itemFirst = Math.trunc(scrollHeightTop.value / props.heightItem)
//     return props.items.slice(itemFirst, itemFirst + countItemRender)
// })

const scrollHeigthBottom = computed(() => {
    const dif = scrollHeightTop.value + (countItemRender * props.heightItem)
    return (props.items.length * props.heightItem) - dif;
})

function scrollY(ev: any) {
  console.log(ev.target.scrollHeight, props.items.length * props.heightItem)
  updateScrollTop(ev.target.scrollTop)
}

function updateScrollTop(scrollTop: number) {
  scrollHeightTop.value = scrollTop;
}
</script>

<template>
    {{ scrollHeightTop + (countItemRender * props.heightItem) + scrollHeigthBottom }}
  <div
    class="content"
    :style="styleContentComputed"
    @scroll="scrollY"
  >
    <div :style="{height: `${scrollHeightTop}px`, background: 'red'}" />

    <div :style="{height: `${countItemRender * props.heightItem}px`, background: 'orange'}" />

    <div :style="{height: `${scrollHeigthBottom}px`, background: 'green'}" />

<!--    <table>-->
<!--&lt;!&ndash;      <thead>&ndash;&gt;-->
<!--&lt;!&ndash;        <tr>&ndash;&gt;-->
<!--&lt;!&ndash;          <td&ndash;&gt;-->
<!--&lt;!&ndash;            v-for="(header, indexColumn) in props.headers"&ndash;&gt;-->
<!--&lt;!&ndash;            :key="indexColumn"&ndash;&gt;-->
<!--&lt;!&ndash;          >&ndash;&gt;-->
<!--&lt;!&ndash;            {{ header.text }}&ndash;&gt;-->
<!--&lt;!&ndash;          </td>&ndash;&gt;-->
<!--&lt;!&ndash;        </tr>&ndash;&gt;-->
<!--&lt;!&ndash;      </thead>&ndash;&gt;-->

<!--      <tbody>-->
<!--&lt;!&ndash;        <tr>&ndash;&gt;-->
<!--&lt;!&ndash;          <td :colspan="props.headers.length" :style="{height: `${scrollHeightTop}px`}" />&ndash;&gt;-->
<!--&lt;!&ndash;        </tr>&ndash;&gt;-->

<!--        <tr-->
<!--          v-for="(item, indexRow) in itemsRender"-->
<!--          :key="indexRow"-->
<!--          :style="styleRowComputed"-->
<!--        >-->
<!--          <td-->
<!--            v-for="(header, indexColumn) in props.headers"-->
<!--            :key="indexColumn"-->
<!--          >-->
<!--            {{ item[header.value] }}-->
<!--          </td>-->
<!--        </tr>-->
<!--      </tbody>-->
<!--    </table>-->
  </div>
</template>

<style scoped>
.content {
    overflow: auto;
}
.content table {
    width: 100%;
    font-size: 11px;
    border-collapse: collapse;
}
</style>
