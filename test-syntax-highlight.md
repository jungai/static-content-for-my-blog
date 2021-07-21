---
name: 'test-syntax-highlight'
title: 'ทดสอบ syntax highlight with @mapbox/rehype-prism'
date: '2021-05-02T09:27:03.295Z'
---

เนื่องจาก jungai.me ใช้ [mdx](https://mdxjs.com/) เป็น base ในการ render markdown จากเว็บแนะนำว่าถ้าจะใช้ [syntax highlighting](https://mdxjs.com/guides/syntax-highlighting) มีอยู่ประมาณ 2 วิธี คือ

1. MdxProvider

```jsx
// src/App.js
import React from 'react'
import {MDXProvider} from '@mdx-js/react'

const components = {
  pre: props => <div {...props} />,
  code: props => <pre style={{color: 'tomato'}} {...props} />
}

export default props => (
  <MDXProvider components={components}>
    <main {...props}></main>
  </MDXProvider>
)
```

สร้าง Provider ขึ้นมา 1 ตัวเพื่อ custom element ที่เราต้องการ map กับตัว markdown โดยอิงจาก [อันนี้](https://mdxjs.com/table-of-components)

2. Remark plugin (ใช้วิธีนี้)

เนื่องจาก jungai.me ใช้ nextjs ใน doc ก็มีวิธีใช้อยู่แล้วตาม[อันนี้](https://mdxjs.com/getting-started/next)

```js
// next.config.js
const rehypePrism = require('@mapbox/rehype-prism')

const withMDX = require('@next/mdx')({
  options: {
    remarkPlugins: [],
    rehypePlugins: [rehypePrism]
  }
})
module.exports = withMDX()
```

แต่ช้าก่อนวิธีข้างบนนี้ใช้ได้ในกรณีที่เราใช้ mdx เพียวๆ แต่ jungai.me ใช้ตัว [next-mdx-remote](https://github.com/hashicorp/next-mdx-remote) ในการโหลดตัว mdx เราจะต้องเพิ่มการใช้งานผ่าน mdxOption จากตัว renderToString ตาม [api](https://github.com/hashicorp/next-mdx-remote#apis)

```js
								...
const source = await renderToString(result.content, {
	mdxOptions: { rehypePlugins: [rehypePrism] },
});
								...
```

หลังจากนั้นก็ไปหา css theme ตามที่เราชอบครับ !! (ผมใช้ตัว `prism-okaidia` )