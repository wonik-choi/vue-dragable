<script setup lang="ts">
import { ref, onMounted, type Ref } from 'vue'
import { useDraggable } from 'vue-draggable-plus'
import { VueDraggable } from 'vue-draggable-plus'
import type { DraggableEvent, UseDraggableOptions, RefOrElement } from 'vue-draggable-plus'

const el = ref()
type test = Exclude<RefOrElement, string>

const array = ref([
  {
    id: 1,
    name: 'John'
  },
  {
    id: 2,
    name: 'Jane'
  },
  {
    id: 3,
    name: 'Doe'
  }
])

useDraggable(el, array, {
  animation: 150,
  ghostClass: 'ghost',
  onStart() {
    console.log('start')
  },
  onUpdate(e) {
    console.log(e.newDraggableIndex)
  }
})
</script>

<template>
  <main>
    <div class="flex flex-col gap-[10rem] justify-center items-center size-full h-lvh">
      <div class="flex flex-col gap-2 p-4 size-full m-auto bg-gray-500/5 rounded" ref="el">
        <div v-for="item in array" :key="item.id" class="w-full p-3 border">
          {{ item.name }}
        </div>
      </div>
      <VueDraggable
        class="flex flex-col gap-2 p-4 size-full m-auto bg-gray-500/5 rounded"
        v-model="array"
      >
        <div v-for="item in array" :key="item.id" class="w-full p-3 border">
          {{ item.name }}
        </div>
      </VueDraggable>
    </div>
  </main>
</template>

<style scoped>
.ghost {
  opacity: 0.5;
  background-color: #f3f4f6;
}
</style>
