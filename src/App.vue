<template>
  <div>
    <h1>WITH ACTIONS</h1>
    <div style="margin-top: 1em">
      <AppSelect :options="options" v-model:select="select" placeholder="Выберите животное"/>
    </div>
  </div>

  <div>
    <AppTable :data="data" :columns="cloumns"/>
  </div>
</template>
<script lang="ts" setup>
import AppSelect from "./components/AppSelect/AppSelect.vue"
import {ref} from "vue";
import AppTable from "./components/AppTable/AppTable.vue";

const select = ref(null)

const options = [
  {
    id: 1,
    title: "Слон"
  },
  {
    id: 2,
    title: "Бегемот"
  },
  {
    id: 3,
    title: "Зебра"
  },
  {
    id: 4,
    title: "Жираф"
  },
  {
    id: 5,
    title: "Лев"
  }
]


const cloumns = [
  {
    field: 'number',
    title: "Номер",
    type: "number"
  }, {
    field: 'developer',
    title: "Девелопер",
    type: "string"
  }, {
    field: 'deadline',
    title: "Срок",
    type: "date"
  }, {
    field: 'type',
    title: "Тип",
    type: "string"
  }, {
    field: 'floor',
    title: "Этаж",
    type: "number"
  }, {
    field: 'square',
    title: "Площадь",
    type: "number"
  },
]

const data = [
  {
    id: 1,
    number: 421,
    developer: 'PRINZIP',
    deadline: '2006-08-09T18:31:42',
    type: 'Студия',
    floor: 2,
    square: 100.3
  },
  {
    id: 2,
    number: 73,
    developer: 'Брусника',
    deadline: '2007-08-09T18:31:42',
    type: '2-к',
    floor: 1,
    square: 10.3
  },
  {
    id: 3,
    number: 122,
    developer: 'TEN',
    deadline: '2001-08-09T18:31:42',
    type: '3-к',
    floor: 2,
    square: 103
  },
  {
    id: 4,
    number: 1,
    developer: 'PRINZIP',
    deadline: '2005-08-09T18:31:42',
    type: 'Студия',
    floor: 2,
    square: 100.3
  },
  {
    id: 5,
    number: 72,
    developer: 'Брусника',
    deadline: '2005-08-09T18:31:42',
    type: '2-к',
    floor: 2,
    square: 10.3
  },
  {
    id: 6,
    number: 23,
    developer: 'TEN',
    deadline: '2005-08-09T18:31:42',
    type: '3-к',
    floor: 2,
    square: 103
  },
  {
    id: 7,
    number: 5,
    developer: 'PRINZIP',
    deadline: '2005-08-09T18:31:42',
    type: 'Студия',
    floor: 2,
    square: 100.3
  },
  {
    id: 8,
    number: 2,
    developer: 'Брусника',
    deadline: '2005-08-09T18:31:42',
    type: '2-к',
    floor: 2,
    square: 10.3
  },
  {
    id: 9,
    number: 97,
    developer: 'TEN',
    deadline: '2005-08-09T18:31:42',
    type: '3-к',
    floor: 2,
    square: 103
  },
  {
    id: 10,
    number: 34,
    developer: 'PRINZIP',
    deadline: '2005-08-09T18:31:42',
    type: 'Студия',
    floor: 2,
    square: 100.3
  },
  {
    id: 11,
    number: 1,
    developer: 'Брусника',
    deadline: '2005-08-09T18:31:42',
    type: '2-к',
    floor: 2,
    square: 10.3
  },
  {
    id: 12,
    number: 88,
    developer: 'TEN',
    deadline: '2003-08-09T18:31:42',
    type: '3-к',
    floor: 2,
    square: 103
  },

]

</script>

