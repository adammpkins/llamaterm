<script setup>
import TheWelcome from '../components/TheWelcome.vue'
import { ref } from 'vue'

const selected = ref('')
selected.value = 'linux'

</script>

<template>
  <main>
    <div class="grid place-items-center mb-20">
      <select v-model="selected" class="select select-bordered w-full max-w-xs">
        <option value="linux" selected>Find a Linux command</option>
        <option value="question">Ask a question</option>

      </select>
    </div>
    <!-- <div class="mockup-code">
      <pre data-prefix="$"><code>ask "list the contents of the current directory"</code></pre>
      <pre data-prefix=">" class="text-success"><code>The command I think you want to run is: ls -l</code></pre>
      <pre data-prefix=">" class="text-success"><code>Would you like to run this command? (Y/n)</code></pre>
      <pre data-prefix=">"><code>Y</code></pre>
      <pre data-prefix=">" class="text-success"><code>Running command...</code></pre>

      <pre><code>total 0</code></pre>
      <pre><code>-rw-r--r-- 1 adammpkins adammpkins 0 Aug 22 05:56 1</code></pre>
    </div> -->
    <div v-if="selected === 'linux'"
    class="border-container grid place-items-center lg:w-[560px] lg:h-[310px] sm:h-[210px] sm:w-[369.33px]">
      <img src="/images/termout.gif" class="cropped lg:h-[300px] sm:h-[200px]" alt="">
    </div>
    <div v-if="selected === 'question'"
    class="border-container grid place-items-center lg:w-[560px] lg:h-[310px] sm:h-[210px] sm:w-[369.33px]">
      <img src="/images/lt-question.gif" class="cropped lg:h-[300px] sm:h-[200px]" alt="">
    </div>


  </main>
</template>
