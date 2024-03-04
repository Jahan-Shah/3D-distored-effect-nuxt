<script setup>
import '@tresjs/leches/styles'

useControls('fpsgraph')
</script>

<template>
  <TresCanvas>
    <TresPerspectiveCamera :position="[0, 0, 2]" :look-at="[0, 0, 0]" />
    <Suspense>
      <MyTorus />
    </Suspense>
    <TresDirectionalLight :intensity="3" :position="[0, 3, 2]" />
    <Environment preset="city" />
  </TresCanvas>
  <TresLeches />
</template>