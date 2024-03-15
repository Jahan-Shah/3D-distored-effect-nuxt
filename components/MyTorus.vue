<script setup>
import { FrontSide, BackSide } from 'three';

const { nodes } = await useGLTF('/torrus.glb')

const { sizes } = useTresContext()
const scale = computed(() => sizes.aspectRatio.value / 1.8)


const { onLoop } = useRenderLoop()
const torusRef = shallowRef()
onLoop(() => {
  if (torusRef.value) {
    torusRef.value.rotation.x += 0.02
  }
})

const { thickness, roughness, transmission, ior, backside } = useControls({
  thickness: { value: 0.2, min: 0, max: 3, step: 0.05 },
  roughness: { value: 0, min: 0, max: 1, step: 0.1 },
  transmission: { value: 1, min: 0, max: 1, step: 0.1 },
  ior: { value: 1.2, min: 0, max: 3, step: 0.1 },
  backside: true,
})

const side = computed(() => backside.value.value ? BackSide : FrontSide)
</script>

<template>
  <TresGroup :scale>
    <Suspense>
      <Text3D font="/fonts/PPNeueMontreal-Bold.json" :curveSegments="10" :size="0.28" :position="[0, 0, -1]"
        :bevelEnabled="false" :height="0">
        hello world!
        <TresMeshBasicMaterial />
      </Text3D>
    </Suspense>
    <primitive ref="torusRef" :object="nodes.Torus002">
      <TresMeshPhysicalMaterial :side :thickness="thickness.value" :roughness="roughness.value"
        :transmission="transmission.value" :ior="ior.value">
      </TresMeshPhysicalMaterial>
    </primitive>
  </TresGroup>
</template>
