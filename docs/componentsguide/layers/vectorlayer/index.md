# ol-vector-layer

ol-vector-layer can render vector from various backend services. It should be used with together with ol-source-vector component.

<script setup>
import VectorSourceDemo1 from "@demos/VectorSourceDemo1.vue"
</script>

<ClientOnly>
<VectorSourceDemo1 />
</ClientOnly>

## Usage

Example below shows how you can use ol-vector-layer and ol-source-vector to render some vector features from remote backend.

Load features simply by providing url value and format GeoJSON

::: code-group

<<< ../../../../src/demos/VectorSourceDemo1.vue

:::

## Properties

### className

- **Type**: `string`
- **Default**: `ol-layer`

A CSS class name to set to the layer element.

### opacity

- **Type**: `number `
- **Default**: `1`

Opacity (0, 1).

### visible

- **Type**: `boolean`
- **Default**: `true`

Visibility.

### extent

- **Type**: `Array`

The bounding extent for layer rendering. The layer will not be rendered outside of this extent.

### zIndex

- **Type**: `number`

The z-index for layer rendering. At rendering time, the layers will be ordered, first by Z-index and then by position.

### minResolution

- **Type**: `number`

The minimum resolution (inclusive) at which this layer will be visible.

### maxResolution

- **Type**: `number`

The maximum resolution (exclusive) below which this layer will be visible.

### minZoom

- **Type**: `number`

The minimum view zoom level (exclusive) above which this layer will be visible.

### maxZoom

- **Type**: `number`

The maximum view zoom level (inclusive) at which this layer will be visible.

### renderBuffer

- **Type**: `number`
- **Default**: `100`
  The buffer in pixels around the viewport extent used by the renderer when getting features from the vector source for the rendering or hit-detection. Recommended value: the size of the largest symbol, line width or label.

### updateWhileAnimating

- **Type**: `Boolean`
- **Default**: `false`
  When set to true, feature batches will be recreated during animations. This means that no vectors will be shown clipped, but the setting will have a performance impact for large amounts of vector data. When set to false, batches will be recreated when no animation is active.

### updateWhileInteracting

- **Type**: `Boolean`
- **Default**: `false`
  When set to true, feature batches will be recreated during interactions. See also updateWhileAnimating.
