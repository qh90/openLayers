# ol-layer-group

> A Collection of layers that are handled together.

<script setup>
import TileJSONDemo from "@demos/TileJSONDemo.vue"
</script>
<ClientOnly>
<TileJSONDemo />
</ClientOnly>

## Usage

The example below shows how you can apply common styles / behavior on multiple layers.

::: code-group

<<< ../../../../src/demos/TileJSONDemo.vue

:::

## Properties

### Props from OpenLayers

Properties are passed-trough from OpenLayers directly.
Their types and default values can be checked-out [in the official OpenLayers docs](https://openlayers.org/en/latest/apidoc/module-ol_layer_Group-LayerGroup.html).
Only some properties deviate caused by reserved keywords from Vue / HTML.
This deviating props are described in the section below.

### Deviating Properties

None.

## Events

You have access to all Events from the underlying source.
Check out [the official OpenLayers docs](https://openlayers.org/en/latest/apidoc/module-ol_layer_Group-LayerGroup.html) to see the available events tht will be fired.

```html
<ol-layer-group :opacity="0.2" @error="handleEvent">
  <!-- ... -->
</ol-layer-group>
```

## Methods

You have access to all Methods from the underlying source.
Check out [the official OpenLayers docs](https://openlayers.org/en/latest/apidoc/module-ol_layer_Group-LayerGroup.html) to see the available methods.

To access the source, you can use a `ref()` as shown below:

```vue
<template>
  <!-- ... -->
  <ol-layer-group :opacity="0.2" ref="layerGroupRef">
    <!-- ... -->
  </ol-layer-group>
  <!-- ... -->
</template>

<script setup lang="ts">
import { ref, onMounted } from "vue";
import type LayerGroup from "ol/layer/LayerGroup";

const layerGroupRef = ref<{ layerGroup: LayerGroup }>(null);

onMounted(() => {
  const layerGroup: LayerGroup = sourceRef.layerGroup;
  // call your method on `layerGroup`
});
</script>
```
