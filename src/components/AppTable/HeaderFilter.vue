<template>
  <button class="header-filter" @click="sortNext">
    <div>
      {{ column.title }}
    </div>
    <div>

      <button @click.stop="sort('desc')" :class="{active: sortType.sortType === 'desc' && sortType.field === column.field}">
        <svg
            transform="rotate(180)"
            xmlns="http://www.w3.org/2000/svg"
            width="8"
            height="8"
            viewBox="0 0 6 5"
            fill="none"
        >
          <path
              opacity="0.3"
              d="M3.43301 4.25L5.16506 1.25C5.35751 0.916667 5.11695 0.5 4.73205 0.5H1.26795C0.883049 0.5 0.642486 0.916666 0.834936 1.25L2.56699 4.25C2.75944 4.58333 3.24056 4.58333 3.43301 4.25Z"
              stroke="#29277D"
              stroke-linejoin="round"
          />
        </svg>

      </button>
      <button @click.stop="sort('asc')" :class="{active: sortType.sortType === 'asc' && sortType.field === column.field}">
        <svg

            xmlns="http://www.w3.org/2000/svg"
            width="8"
            height="8"
            viewBox="0 0 6 5"
            fill="none"
        >
          <path

              opacity="0.3"
              d="M3.43301 4.25L5.16506 1.25C5.35751 0.916667 5.11695 0.5 4.73205 0.5H1.26795C0.883049 0.5 0.642486 0.916666 0.834936 1.25L2.56699 4.25C2.75944 4.58333 3.24056 4.58333 3.43301 4.25Z"
              stroke="#29277D"
              stroke-linejoin="round"
          />
        </svg>

      </button>
    </div>
  </button>
</template>

<script setup lang="ts">
type SortType = {
  field: null | string,
  sortType: "asc" | "desc" | null
}


const props = defineProps<{
  column:
      { field: string, title: string, type: string },
  sortType: SortType
}>()

const emit = defineEmits<{
  // @ts-ignore
  (e: "update:sortType", sortType: SortType)
}>()

function sort(sort: "asc" | "desc") {
  emit("update:sortType", {
    sortType: sort,
    field: props.column.field
  })
}

function sortNext() {
  if (props.sortType.field !== props.column.field) {
    return emit("update:sortType", {sortType: "asc", field: props.column.field})
  }
  switch (props.sortType.sortType) {
    case "asc":
      return emit("update:sortType", {sortType: "desc", field: props.column.field})
    case "desc":
      return emit("update:sortType", {sortType: null, field: null})
    case null:
      return emit("update:sortType", {sortType: "asc", field: props.column.field})
    default:
      return null
  }
}

</script>

<style scoped>
button {
  display: block;
  text-align: left;
  border: none;
  background: none;
}

.header-filter {
  --active: #29277d;
  display: flex;
  align-items: center;
  width: 100%;
  justify-content: space-between;
}

.active svg {
  fill: var(--active);
}

</style>