<template>
  <div class="table-wrapper">
    <table class="table">
      <thead>
      <tr class="header-row">
        <td class="header-cell" v-for="col in columns" :key="col.field">
          <HeaderFilter :column="col" v-model:sortType="sortType"/>
        </td>
      </tr>
      </thead>
      <tbody>
      <tr v-for="string in compData" :key="string.id" class="row">
        <td class="cell" v-for="col in columns" :key="col.field">{{ string[col.field] }}</td>
      </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup lang="ts">

import {computed, ref} from "vue";
import HeaderFilter from "./HeaderFilter.vue";

const props = defineProps<{
  data: {
    id: number,
    number: number,
    developer: string,
    deadline: string,
    type: string,
    floor: number,
    square: number
  }[],
  columns:
      { field: string, title: string, type: string }[]
}>()
const sortType = ref({
  field: null,
  sortType: null
})
const compData = computed(() => {
  const arr = [...props.data]
  const {field, sortType:sorting} = sortType.value

  if(field) {
    const index = props.columns.findIndex(item=>item.field === field)
    if (index > -1) {
      const sortingType = props.columns[index].type
      if (sortingType === "string") {
        return arr.sort((a, b)=>{
          if(sorting === "asc") {
            return a[field].toLowerCase().localeCompare(b[field])
          } else if (sorting === "desc") {
            return b[field].toLowerCase().localeCompare(a[field])
          }
        })
      } else if(sortingType === "date") {
        return arr.sort((a, b)=>{
          const aDate = new Date(a[field])
          const bDate = new Date(b[field])
          if(sorting === "asc") {

            return aDate - bDate
          } else if (sorting === "desc") {
            return bDate -  aDate
          }
        })
      } else if(sortingType === "number") {
        return arr.sort((a, b)=>{
          if(sorting === "asc") {
            return a[field] - b[field]
          } else if (sorting === "desc") {
            return b[field] - a[field]
          }
        })
      } else {
        return props.data
      }
    }
  } else {
    return props.data
  }

})



</script>

<style scoped>
* {
  box-sizing: border-box;
}

.table-wrapper {
  height: 400px;
  overflow: auto;
  position: relative;
  border: 2px solid darkgray;
}

.table {
  width: 100%;
  height: 600px;
  border-collapse: separate;
  border-spacing: 0;
}


.header-row {
  height: 48px;
  position: sticky;
  top: 0;
  background: white;
}

.header-cell {
  border-bottom: 1px solid black;
  font-weight: bold;
  text-transform: capitalize;
}

.row:nth-child(2n+1) {
  background: lightgray;
}

.row:not(:last-child) > .cell {
  border-bottom: 1px solid darkgray;
}

.cell {
  height: 40px;
}
</style>