<template>
  <div class="w-screen h-screen bg-black">
    <draggable v-model="items" :move="onMove">
      <div v-for="(item, index) in items" :key="item.id" class="flex items-center justify-center w-32 h-32 bg-white border-2 border-gray-200 rounded-lg">
        <img :src="item.image" class="w-24 h-24">
        <span class="text-gray-500">{{ item.name }}</span>
      </div>
    </draggable>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import draggable from 'vue-draggable'
import { invoke } from '@tauri-apps/api'
export default defineComponent({
  name: 'TierList',
  components: { draggable },
  data() {
    return {
      items: [
        { id: 1, name: 'Item 1', image: 'path/to/image1.jpg' },
        { id: 2, name: 'Item 2', image: 'path/to/image2.jpg' },
        { id: 3, name: 'Item 3', image: 'path/to/image3.jpg' },
        { id: 4, name: 'Item 4', image: 'path/to/image4.jpg' },
        { id: 5, name: 'Item 5', image: 'path/to/image5.jpg' }
      ]
    }
  },
  methods: {
    onMove(event: any) {
      // Get the item being dragged
      const item = this.items[event.draggedContext.index]
      // Get the target index
      const targetIndex = event.relatedContext.index
      // Move the item to the new index
      this.items.splice(event.draggedContext.index, 1)
      this.items.splice(targetIndex, 0, item)
    }
  }
})
</script>
