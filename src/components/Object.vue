<script setup>
import { ref } from 'vue'
import { NCascader } from 'naive-ui'
import areaList from '../utils/area.json'
const options = ref(areaList)

const flatOption = ref([])

const handleFlat = (arr) => {
    arr.forEach(item => {
        if (item.children && item.children.length !== 0) {
            handleFlat(item.children)
            item.children = []
        }
        flatOption.value.push(item)
    })
}

handleFlat(options.value)

const getCascaderOptions = (arr) => {
    return arr.filter(item => item.level !== 3).map(item => {
        return {
            ...item,
            children: !item.city_code && arr.filter(child => child.pcode == item.value)
        }
        // if (item.pcode) {
        //     const index = arr.findIndex(child => child.value === item.pcode)
        //     arr[index].children.push(item)
        // }
    })
}

const handleRecursive = (arr, pcode) => {
    return arr.filter(item => item.pcode === pcode).map(item => {
        const children = handleRecursive(arr, item.value)
        return {
            ...item,
            children
        }
    })
}
console.time('time')
console.log(handleRecursive(flatOption.value), '我是flatOption');
console.timeEnd('time')

</script>

<template>
    <!-- <n-cascader
        v-model:value="value"
      placeholder="没啥用的值"
      :expand-trigger="hoverTrigger ? 'hover' : 'click'"
      :options="options"
      :check-strategy="checkStrategyIsChild ? 'child' : 'all'"
      :show-path="showPath"
      :filterable="filterable"
      @update:value="handleUpdateValue"
    /> -->
</template>

<style lang='scss' scoped>
</style>