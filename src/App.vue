<script setup lang="ts">
import { useCssVar } from '@vueuse/core';
import { useTemplateRef } from 'vue';

const elem = useTemplateRef("elem")
const colorRef = useCssVar("--elemColor", elem)
const colorNoRef = useCssVar("--rootColor")
const colorNoRefObserve = useCssVar("--rootColor", undefined, {observe: true})
const colorUndefinedWithInitial = useCssVar("--rootColorTwo", undefined, {initialValue: "blue"})

function color(c: string | undefined) {
  return "color: " + c
}
</script>


<template>
  <div ref="elem" id="elem">
    <p>
      Color without ref and no initial is <span :style="color(colorNoRef)">[{{ colorNoRef }}]</span>
    </p>
    <p>
      Color without ref, no initial and observe is <span :style="color(colorNoRefObserve)">[{{ colorNoRefObserve }}]</span>
    </p>
    <p>
      Color without ref and initial is <span :style="color(colorUndefinedWithInitial)">[{{ colorUndefinedWithInitial }}]</span>
    </p>
    <p>
      Color with ref is <span :style="color(colorRef)">[{{ colorRef }}]</span>
    </p>
  </div>
</template>

<style lang="css">
:root {
  --rootColor: red;
  --rootColorTwo: blue;
}

#elem {
  --elemColor: green;
}
</style>
