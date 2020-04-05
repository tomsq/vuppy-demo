<template>
  <div class="h-screen">
    <h1 class="pt-10 flex justify-center text-4xl text-gray-800">Vuppy - Demo</h1>

    <div class="md:flex md:w-full md:justify-around items-center pt-16 px-8">
      <div class="w-full md:w-1/2 flex justify-center">
        <vuppy class="pb-16" v-model="images" :dashboardHeight="400" :dashboardWidth="600"></vuppy>
      </div>

      <div class="w-full md:w-1/2">

        <a @click="images = []" class="bg-teal-700 text-white px-4 py-2 rounded cursor-pointer hover:bg-teal-600">Clear Images Externally</a>

        <div class="mt-10 overflow-y-auto overflow-x-auto bg-gray-400 rounded" style="height: 33rem;">
          <json-view class="pt-4 pl-4" :data="strippedData" :max-depth="3" rootKey="images"/>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

import vuppy from 'vuppy'
import { JSONView } from 'vue-json-component';


export default {
  components: {
    vuppy,
    'json-view': JSONView
  },

  data() {
    return {
      images: []
    }
  },

  computed: {
    strippedData() {
      let strippedData = []
      this.images.forEach(image => {
        strippedData.push({
          file: image.file.substring(0,32) + '...',
          id: image.id,
          name: image.name
        })
      });

      return strippedData;
    }
  }

}
</script>
