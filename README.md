# vue-virtual-draglist

[![npm](https://img.shields.io/npm/v/vue-virtual-draglist.svg)](https://www.npmjs.com/package/vue-virtual-draglist)  [![npm](https://img.shields.io/npm/dt/vue-virtual-draglist.svg)](https://www.npmjs.com/package/vue-virtual-draglist)  [![vue2](https://img.shields.io/badge/vue-2.x-brightgreen.svg)](https://vuejs.org/)

A virtual scrolling list component that can be sorted by dragging

For Vue 3 support, see [here](https://github.com/mfuu/vue3-virtual-drag-list)

### [Live demo](https://mfuu.github.io/vue-virtual-drag-list/)

## Simple usage

```bash
npm i vue-virtual-draglist
```

Root component:
```vue
<template>
  <div>
    <!--
      :draggable="'div'" // use tagName 
      :draggable="'.item'" // use class
      :draggable="'#item'" // use id
    -->
    <virtual-drag-list
      :data-key="'id'"
      :data-source="list"
      :draggable="'.item'"
      :handle="'.handle'"
      :item-class="'item'"
      style="height: 500px"
      @top="handleToTop"
      @bottom="handleToBottom"
      @drag="onDrag"
      @drop="onDrop"
      @add="onAdd"
      @remove="onRemove"
    >
      <template slot="item" slot-scope="{ record, index, dataKey }">
        <span class="handle">{{ record.id }}</span>
        {{ record.text }}
      </template>
      <template slot="header">
        <div class="loading">top loading...</div>
      </template>
      <template slot="footer">
        <div class="loading">bottom loading...</div>
      </template>
    </virtual-drag-list>
  </div>
</template>

<script>
  import virtualDragList from 'vue-virtual-draglist'

  export default {
    name: 'root',
    components: { virtualDragList },
    data () {
      return {
        list: [{id: '1', text: 'asd'}, {id: '2', text: 'fgh'}, ...]
      }
    },
    methods: {
      handleToTop() {
        // code here
      },
      handleToBottom() {
        // code here
      },
      onDrag({ list, from }) {
        // code here
      },
      onDrop({ list, from, to, changed }) {
        // code here
      },
      onAdd({ item, key, index }) {
        // code here
      },
      onRemove({ item, key, index }) {
        // code here
      }
    }
  }
</script>
```
## Emits

|   **Emit**   | **Description** |
|--------------|-----------------|
| `top`        | Event fired when scroll to top |
| `bottom`     | Event fired when scroll to bottom |
| `drag`       | Event fired when the drag is started |
| `drop`       | Event fired when the drag is completed |
| `add`        | Event fired when element is dropped into the list from another |
| `remove`     | Event fired when element is removed from the list into another |

## Props

### Required props

| **Prop** | **Type**  | **Description** |
|------------------|-------------|------------------|
| `data-key`       | String      | The unique identifier of each piece of data, in the form of `'a.b.c'` |
| `data-source`    | Array       | data list  |

### Optional props

**Commonly used**

|   **Prop**   |  **Type**  | **Default** | **Description** |
| ------------ | ---------  | ----------- | --------------- |
| `keeps`      | `Number`   | `30`        | The number of lines rendered by the virtual scroll |
| `size`       | `Number`   | `-`         | The estimated height of each piece of data, you can choose to pass it or not, it will be automatically calculated |
| `direction`  | `String`   | `vertical`  | `vertical/horizontal`, scroll direction |
| `draggable`  | `Function/String` | `-`  | Specifies which items inside the element should be draggable |
| `handle`     | `Function/String` | `-`  | Drag handle selector within list items |
| `group`      | `Function/String` | `-`  | string: 'name' or object: `{ name: 'group', put: true/false, pull: true/false }` |
| `keepOffset` | `Boolean`  | `false`     | When scrolling up to load data, keep the same offset as the previous scroll |


**Uncommonly used**

|  **Prop**    | **Type**   | **Default** | **Description** |
|  --------    | --------   | ----------- | --------------- |
| `disabled`   | `Boolean`  | `false`     | Disables the sortable if set to true |
| `delay`      | `Number`   | `0`        | Delay time of debounce function |
| `animation`  | `Number`   | `150`       | Animation speed moving items when sorting |
| `autoScroll` | `Boolean`  | `true`      | Automatic scrolling when moving to the edge of the container |
| `scrollThreshold` | `Number` | `25`     | Threshold to trigger autoscroll |
| `rootTag`    | `String`   | `div`       | Label type for root element |
| `wrapTag`    | `String`   | `div`       | Label type for list wrap element |
| `itemTag`    | `String`   | `div`       | Label type for list item element |
| `headerTag`  | `String`   | `div`       | Label type for header slot element |
| `footerTag`  | `String`   | `div`       | Label type for footer slot element |
| `wrapClass`  | `String`   | `''`        | List wrapper element class |
| `wrapStyle`  | `Object`   | `{}`        | List wrapper element style |
| `itemClass`  | `String`   | `''`        | List item element class |
| `itemStyle`  | `Object`   | `{}`        | List item element style |
| `ghostClass` | `String`   | `''`        | The class of the mask element when dragging |
| `ghostStyle` | `Object`   | `{}`        | The style of the mask element when dragging |
| `chosenClass`| `String`   | `''`        | The class of the selected element when dragging |

## Methods

Use <code><a href="https://vuejs.org/v2/guide/components-edge-cases.html#Accessing-Child-Component-Instances-amp-Child-Elements">ref</a></code> to get the method inside the component


| **Method**         | **Description** |
| ------------------ | --------------- |
| `reset()`          | Reset to initial |
| `getSize(key)`     | Get the size of the current item by unique key value |
| `getOffset()`      | Get the current scroll height |
| `scrollToTop()`    | Scroll to top of list |
| `scrollToBottom()` | Scroll to bottom of list |
| `scrollToIndex(index)`  | Scroll to the specified index position |
| `scrollToOffset(offset)` | Scroll to the specified offset |


## License

[MIT License.](https://github.com/mfuu/vue-virtual-drag-list/blob/main/LICENSE)
