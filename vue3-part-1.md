---
name: 'vue3-part-1'
title: 'มาดู feature ของ vue3 กัน part 1'
date: '2021-05-02T17:54:49.153Z'
---

หลังจากที่ [vue3](https://v3.vuejs.org/) เป็น official มาสักพักแล้วเรามาลองดู feature ใหม่ๆใน vue3 และสิ่งที่เปลี่ยนไปจาก vue2 กันอาจจะไม่ cover ทั้งหมดจะทยอยเพิ่มเติมให้ครับ

### Multi Root Node (Feature)

เป็น feature ที่ผมชอบมากครับจริงๆแล้วมันคือ fragment ใน react 

```html
// Hero.vue
<template>
	<!-- Hero Component -->
	<h1>Hello</h1>
	<h2>Vue3</h2>
</template>
```

**NOTE**

เวลาใช้งาน component ที่เป็น fragment จะไม่สามารถใช้พวก directives ได้เนื่องจากตอนมันไป render แล้วไม่มี root element

```html
<template>
	<Hero v-if="false"/>
	<Hero v-show="false" />
</template>
```

### Custom Component with v-model (Breaking Change)

แน่นอนครับเวลาเราจะเรียกใช้ v-model ใน custom component เราจะส่งค่า value ผ่าน props และรับค่า emit value

#### vue 2

```html
<template>
  <div>
     <h1>{{ value }}</h1>
    <button type="button" @click="handleClick">click</button>
  </div>
</template>

<script>
export default {
  props: {
    value: {
        type: String, // up to you
        default: undefined
    },
  },
  methods: {
    handleClick() {
        this.$emit('input', 'iu ❤️')
    }
  }
}
</script>
```

เรียกใช้

```html
<template>
  <div>
    <SomeComponent v-model="msg" />
    <!-- or -->
    <SomeComponent :value="msg" @input="val => msg = val" />
  </div>
</template>

<script>
import SomeComponent from './components/SomeComponent.vue'

export default {
  components: {
    SomeComponent,
  },
  data: () => ({
      msg: 'i love someone'
  }),
}
</script>
```

#### vue 3

```html
// SomeComponent.vue
<template>
    <h1>{{ modelValue }}</h1>
    <button type="button" @click="handleClick">click</button>
</template>

<script>
export default {
    props: {
        modelValue: {
            type: String, // up to you
            default: undefined
        },
    },
    setup(_props, { emit }) {
        const handleClick = () => {
            emit('update:modelValue', 'iu ❤️')
        }
        return { handleClick }
    }
}
</script>
```

เรียกใช้

```html
<template>
	<SomeComponent v-model="msg" />
		<!-- or -->
	<SomeComponent :modelValue="msg" @update:modelValue="val => msg = val" />
</template>

<script>
import { ref } from 'vue'
import SomeComponent from './components/SomeComponent.vue'

export default {
	components: {
		SomeComponent
	},
	setup() {
		const msg = ref('i love someone')

		return { msg }
	}
}
</script>
```
จะสังเกตได้ว่าสิ่งที่เปลี่ยนแปลงไปก็คือ props `value` เป็น `modelValue` และ emit event จาก `input` เป็น `update:modelValue`
เมื่อลองรันโค้ดดูแล้วจะรู้ว่าผมชอบใครอยู่ทั้ง vue2 และ vue3 จะให้คำตอบที่เหมือนกัน(แน่นอน ผมรักเดียว อิอิ)

ก็ขอจบ part 1 ไว้เท่านี้ก่อนแล้วผมจะค่อยๆทำ part ต่อไปมาเรื่อยๆ ครับผม Happy Coding ครับ 🥳