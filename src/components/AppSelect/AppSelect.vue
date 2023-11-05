<template>
  <div class="wrapper" ref="selectRef">
    <div class="select-container" :style="{zIndex}">
      <div class="placeholder" :class="value ? 'top' : 'center'">{{ placeholder }}</div>
      <div class="ovrfl">
        <button class="select" @click="toggleOpen">
          <div>
            {{ value }}
          </div>
          <svg :class="{isOpen}" width="16" height="16" viewBox="0 0 16 16" fill="none"
               xmlns="http://www.w3.org/2000/svg">
            <path d="M3 6L8 11L13 6" stroke="#5F88F4" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
          </svg>
        </button>
        <div class="options" :class="{isOpen}" :style="{height: isOpen? dropDownHeight: 0}"
             @transitionend="ontransitionend">
          <div ref="optionsRef">
            <button class="option" v-for="item in options" :key="item.id" @click="$event=>select(item.id)">
              {{ item.title }}
            </button>
          </div>
        </div>
      </div>

    </div>
  </div>
</template>
<script lang="ts" setup>
import {computed, onMounted, ref, watch} from "vue";

const props = defineProps<{
  select: null | number,
  options: { id: number, title: string }[]
  placeholder: string
}>()

const emit = defineEmits<{
  (e: "update:select", select: null | number)
}>()

const value = computed(() => {
  const index = props.options.findIndex(item => item.id === props.select)
  if (index > -1) {
    return props.options[index].title
  } else {
    return ""
  }
})


const isOpen = ref(false)
const optionsRef = ref()
const dropDownHeight = ref("0px")

function toggleOpen() {
  isOpen.value = !isOpen.value
  if (isOpen.value) {
    zIndex.value = 999
  }
}

function select(id: number) {
  emit('update:select', id)
  isOpen.value = false
}

const zIndex = ref(0)

function ontransitionend() {
  if (!isOpen.value) {
    zIndex.value = 0
  }
}

const selectRef = ref<HTMLElement>()

function closeDropdown(e: Event) {
  let element = e.target as HTMLElement | null
  while (element !== null && element !== selectRef.value) {
    element = element.parentElement
  }
  if (element !== selectRef.value) {
    isOpen.value = false
  }
}

onMounted(() => {
  dropDownHeight.value = optionsRef.value.clientHeight + "px"
})
watch(isOpen, (val) => {
  if (val) {
    document.documentElement.addEventListener("mouseup", closeDropdown)
  } else {
    document.documentElement.removeEventListener("mouseup", closeDropdown)
  }
})

</script>

<style scoped>
button {
  border: none;
  background: none;
  display: block;
}


.wrapper {
  --border: #F968bf;
  --text: #29277d;
  --bg-hover: #DADEFE;
  --placeholder: rgba(41, 39, 125, 0.40);
  --icon: #5F88F4;

  box-sizing: border-box;
  height: 42px;
  color: var(--text);
  position: relative;
}


.select-container {
  width: 400px;
  position: absolute;
}

.ovrfl {
  overflow: hidden;
  border: 1px solid var(--border);
  border-radius: 10px;
  background: white;
}

.select {
  display: block;
  padding: .5em 1em;
  width: 100%;
  text-align: left;
  height: 40px;
}

.placeholder {
  position: absolute;
  color: var(--placeholder);
  z-index: 1;
  transition: all .1s;
  pointer-events: none;
}

.placeholder.top {
  top: -8px;
  left: 1em;
  padding: 0;
  line-height: 1em;
  background: white;
}

.placeholder.center {
  top: .5em;
  left: 1em;
}

.options {
  transition: height .1s;
  overflow: hidden;
}

.options.isOpen {
}

.option {
  display: block;
  padding: .5em 1em;
  width: 100%;
  text-align: left;
}

.option:first-child {
  border-top: 1px solid var(--border);
}

.option:hover {
  background: var(--bg-hover);
}

svg {
  position: absolute;
  top: 14px;
  right: 1em;
  transform: rotate(180deg);
  transition: transform .1s;
}

svg.isOpen {
  transform: rotate(0deg);
}
</style>