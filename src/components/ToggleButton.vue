<template>
<div>
  <!-- Toggle Button -->
  <label 
    for="toogleA"
    class="flex items-center cursor-pointer"
  >
    <!-- toggle -->
    <div class="relative">
      <!-- input -->
      <input id="toogleA" type="checkbox" class="hidden" :value="value" @input="valueChanged" />
      <!-- line -->
      <div
        class="toggle__line w-10 h-4 bg-gray-400 rounded-full shadow-inner"
      ></div>
      <!-- dot -->
      <div
        class="toggle__dot absolute w-6 h-6 bg-white rounded-full shadow inset-y-0 left-0"
      ></div>
    </div>
    <!-- label -->
    <div
      class="ml-3 text-gray-200 font-medium"
    >
       {{ buttonText }}
    </div>
  </label>
  
</div>
</template>

<script>
export default {
    props: {
        value: {
            type: Boolean,
            default: false
        }
    },
    methods: {
        valueChanged(e) {
            this.$emit('input', e.target.checked);
        }
    },

    computed: {
        buttonText() {
            if(this.value) {
                return 'Toggle Mobile';
            } else {
                return 'Toggle Desktop';
            }
        }
    }
}
</script>

<style scoped>
.toggle__dot {
  top: -.25rem;
  left: -.25rem;
  transition: all 0.3s ease-in-out;
}

input:checked ~ .toggle__dot {
  transform: translateX(100%);
}
</style>