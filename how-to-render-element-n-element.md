---
name: 'how-to-render-element-n-element'
title: 'render element n element ใน react'
date: '2021-05-31T13:17:56.453Z'
---

ก่อนอื่นเลยผมเขียน **vue** มาตลอดเวลาผมจะ loop element ตามจำนวนที่ผมต้องการผมก็แค่ใช้ **directive v-for** ของ vue

```html
<div>
	<ul>
		<li v-for="(item, index) in 1000" :key="index"> {{`name${index}`}}</li>
	</ul>
</div>
```

ทีนี้พอมาได้มาลองเขียน  **react** แน่นอนเราไม่ได้เขียน html ใน template แต่กลายมาเป็น **{j,t}sx** เราต้อง loop element เองเพราะไม่มี directive
พอคิดได้ก็ลงมือเขียนเลยย

```jsx
const something = () => (
<div>
	<ul>
		{
			new Array(1000).map((_item, index) => (
				<li key={index}>{`name${index}`}</li>
			))
		}
	</ul>		
</div>
)
```

เย้........

จากโค้ดข้างบนผลลัพธ์ได้ไม่ตรงกับที่ผมคิดไว้เพราะมันไม่ render อะไรเลยเกิดอะไรขึ้นกันแน่เลยมานั้งเช็คดูด้วยการ Log ดูค่า ปรากฏว่า

```new Array(arraySize)``` ผลลัพธ์มันได้ที่ผมต้องการนะว่าสร้าง array ที่มี length เท่ากับ 1000 แต่มันเป็น [empty*1000] และไม่สามารถ **iterate** ได้ (อันนี้เพิ่งรู้เลยนะเนี่ย!!!) พอรู้แบบนี้แล้วก็เลยจำเป็นต้อง spread มันออกมา

```jsx
const something = () => (
<div>
	<ul>
		{
			[...new Array(1000)].map((_item, index) => (
				<li key={index}>{`name${index}`}</li>
			))
		}
	</ul>		
</div>
)
```

เพียงเท่านี้ก็ได้ผลลัพธ์ตามที่ผมต้องการแล้วและก็ได้ความเข้าใจใหม่เพิ่มขึ้นมาอีก