## Timeline

Visually display timeline.

### Basic usage

Timeline can be split into multiple activities in ascending or descending. Timestamps are important features that distinguish them from other components. Note the difference with Steps.

:::demo
```html
<div class="block">
  <div class="radio">
    Order: 
    <ami-radio-group v-model="reverse">
      <ami-radio :label="true">descending</ami-radio>
      <ami-radio :label="false">ascending</ami-radio>
    </ami-radio-group>
  </div>

  <ami-timeline :reverse="reverse">
    <ami-timeline-item
      v-for="(activity, index) in activities"
      :key="index"
      :timestamp="activity.timestamp">
      {{activity.content}}
    </ami-timeline-item>
  </ami-timeline>
</div>

<script>
  export default {
    data() {
      return {
        reverse: true,
        activities: [{
          content: 'Event start',
          timestamp: '2018-04-15'
        }, {
          content: 'Approved',
          timestamp: '2018-04-13'
        }, {
          content: 'Success',
          timestamp: '2018-04-11'
        }]
      };
    }
  };
</script>
```
:::

### Custom node

Size, color, and icons can be customized in node.

:::demo

```html
<div class="block">
  <ami-timeline>
    <ami-timeline-item
      v-for="(activity, index) in activities"
      :key="index"
      :icon="activity.icon"
      :type="activity.type"
      :color="activity.color"
      :size="activity.size"
      :timestamp="activity.timestamp">
      {{activity.content}}
    </ami-timeline-item>
  </ami-timeline>
</div>

<script>
  export default {
    data() {
      return {
        activities: [{
          content: 'Custom icon',
          timestamp: '2018-04-12 20:46',
          size: 'large',
          type: 'primary',
          icon: 'ami-icon-more'
        }, {
          content: 'Custom color',
          timestamp: '2018-04-03 20:46',
          color: '#0bbd87'
        }, {
          content: 'Custom size',
          timestamp: '2018-04-03 20:46',
          size: 'large'
        }, {
          content: 'Default node',
          timestamp: '2018-04-03 20:46'
        }]
      };
    }
  };
</script>
```
:::

### Custom timestamp

Timestamp can be placed on top of content when content is too high.

:::demo

```html
<div class="block">
  <ami-timeline>
    <ami-timeline-item timestamp="2018/4/12" placement="top">
      <ami-card>
        <h4>Update Github template</h4>
        <p>Tom committed 2018/4/12 20:46</p>
      </ami-card>
    </ami-timeline-item>
    <ami-timeline-item timestamp="2018/4/3" placement="top">
      <ami-card>
        <h4>Update Github template</h4>
        <p>Tom committed 2018/4/3 20:46</p>
      </ami-card>
    </ami-timeline-item>
    <ami-timeline-item timestamp="2018/4/2" placement="top">
      <ami-card>
        <h4>Update Github template</h4>
        <p>Tom committed 2018/4/2 20:46</p>
      </ami-card>
    </ami-timeline-item>
  </ami-timeline>
</div>
```
:::

### Timeline Attributes
| Attribute      | Description    | Type      | Accepted Values | Default   |
|---------- |-------- |---------- |-------------  |-------- |
| reverse | whether the node is ascending or descending, default is ascending | boolean | — | false |

### Timeline-item Attributes
| Attribute      | Description    | Type      | Accepted Values | Default   |
|---------- |-------- |---------- |-------------  |-------- |
| timestamp     | timestamp content | string  | - | — |
| hide-timestamp  | whether to show timestamp | boolean | — | false |
| placement | position of timestamp | string | top / bottom | bottom |
| type | node type | string | primary / success / warning / danger / info | - |
| color | background color of node | string | hsl / hsv / hex / rgb | - |
| size | node size | string | normal / large | normal |
| icon | icon class name | string | — | - |

### Timeline-Item Slot
| name | Description |
|------|--------|
| — | Custom content for timeline item |
| dot | Custom defined node |
