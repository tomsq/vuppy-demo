<template>
  <div>
    <div class="h-screen hidden sm:block">
      <split-pane  @resize="resize" :min-percent="20" :default-percent="50" split="vertical">
        <template slot="paneL">
          <div class="flex justify-start pl-8 pt-10">
            <toggle-button :value="mobileToggle" @input="mobileToggled"></toggle-button>
          </div>
          <div class="pt-48 px-8">
            <vuppy v-model="images"></vuppy>
          </div>
        </template>
        <template slot="paneR"> 
          <div class="bg-gray-200 h-screen">
            <h1 class="pt-8 flex justify-center text-4xl text-gray-700">Vuppy - Demo</h1>
            <div class="flex justify-center pt-8 shadow-md pb-6">
              <a @click="images = []" class="bg-teal-700 text-white px-4 py-2 rounded cursor-pointer hover:bg-teal-600">Clear Images Externally</a>
            </div>
            <div class="overflow-y-auto overflow-x-auto  rounded" style="height: 46rem;">
              <json-view class="pt-4 pl-4" :data="strippedData" :max-depth="3" rootKey="images"/>
            </div>
          </div>
        </template>    
      </split-pane>
    </div>
    <div class="h-screen sm:hidden">
      <h1 class="pt-8 flex justify-center text-4xl text-gray-200">Vuppy - Demo</h1>

      <div class="pt-12 px-8">
        <vuppy v-model="images"></vuppy>
      </div>

      <div class="bg-gray-200 mt-20">
        <div class="flex justify-center pt-8 shadow-md pb-6">
          <a @click="images = []" class="bg-teal-700 text-white px-4 py-2 rounded cursor-pointer hover:bg-teal-600">Clear Images Externally</a>
        </div>
        <div class="overflow-y-auto overflow-x-auto  rounded" style="height: 46rem;">
          <json-view class="pt-4 pl-4" :data="strippedData" :max-depth="3" rootKey="images"/>
        </div>
      </div>
    </div>
  </div>
</template>
<script>

import vuppy from 'vuppy';
import { JSONView } from 'vue-json-component';
import splitPane from 'vue-splitpane';
import ToggleButton from './components/ToggleButton';

export default {
  components: {
    vuppy,
    'json-view': JSONView,
    splitPane,
    ToggleButton
  },

  data() {
    return {
      images: [],
      mobileToggle: false
    }
  },

  methods: {
    resize() {
      if (this.$children[0].percent > 50) 
        { this.$children[0].percent = 50 }
    },
    mobileToggled() {
      this.mobileToggle = !this.mobileToggle;

      if(this.mobileToggle === true) {
        this.$children[0].percent = 20;
      } else {
        this.$children[0].percent = 50;
      }
    }
  },

  computed: {
    strippedData() {
      let strippedData = []
      this.images.forEach(image => {
        strippedData.push({
          file: image.file.substring(0,50) + '...',
          id: image.id,
          name: image.name
        })
      });
      return strippedData;
    }
  }
}
</script>
