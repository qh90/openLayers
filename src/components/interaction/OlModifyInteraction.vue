<template>
  <slot></slot>
</template>

<script setup lang="ts">
import type { Ref } from "vue";
import { provide, inject, watch, onMounted, onUnmounted, toRefs } from "vue";
import type Collection from "ol/Collection";
import Modify from "ol/interaction/Modify";
import type Map from "ol/Map";
import type VectorSource from "ol/source/Vector";
import type Geometry from "ol/geom/Geometry";
import type Feature from "ol/Feature";
import type { Condition } from "ol/events/condition";

const props = withDefaults(
  defineProps<{
    condition?: Condition;
    deleteCondition?: Condition;
    insertVertexCondition?: Condition;
    pixelTolerance?: number;
    wrapX?: boolean;
    hitDetection?: boolean;
    features?: Collection<Feature<Geometry>>;
  }>(),
  {
    pixelTolerance: 10,
    wrapX: false,
  }
);

const emit = defineEmits(["modifystart", "modifyend"]);

const map = inject<Map>("map");
const source = inject<Ref<VectorSource> | null>("vectorSource");

const {
  features,
  condition,
  deleteCondition,
  insertVertexCondition,
  pixelTolerance,
  wrapX,
  hitDetection,
} = toRefs(props);

function createModify() {
  const m = new Modify({
    source: source?.value,
    features: features?.value,
    condition: condition?.value,
    deleteCondition: deleteCondition?.value,
    insertVertexCondition: insertVertexCondition?.value,
    pixelTolerance: pixelTolerance.value,
    wrapX: wrapX.value,
    hitDetection: hitDetection.value,
  });

  m.on("modifystart", (event) => {
    emit("modifystart", event);
  });

  m.on("modifyend", (event) => {
    emit("modifyend", event);
  });

  return m;
}

let modify = createModify();

watch(
  [
    condition,
    deleteCondition,
    insertVertexCondition,
    pixelTolerance,
    wrapX,
    hitDetection,
  ],
  () => {
    modify.dispose();
    map?.removeInteraction(modify);
    modify = createModify();
    map?.addInteraction(modify);
    map?.changed();
  }
);

onMounted(() => {
  map?.addInteraction(modify);
});

onUnmounted(() => {
  map?.removeInteraction(modify);
});

provide("stylable", modify);

defineExpose({
  modify,
});
</script>
