---
name: "google-zx"
title: "มิติใหม่ในการเขียน shell script ด้วย google zx"
date: "2021-05-16T08:30:37.917Z"
---

## What is zx

[zx](https://github.com/google/zx) มันคือ tool ที่ใช้ javascript ในการเขียน shell script ครับ เพิ่งมาใหม่ได้ไม่นานและมันติด trend ใน github และ ยอด github star พุ่งขึ้นเร็วมากจนทำให้ตัวผมนั้นอยากลองเลยมาเป็นบทความนี้ครับ

## Background

ตัวผมนั้นไม่ค่อยได้เขียน shell script เวลาไปอ่านรู้สึกได้ว่าค่อนข้างงงเลยครับ (เป็นเพราะว่าตัว syntax ด้วยครับ) และไม่ได้มีเวลาลองจับจริงจังสักที พอเห็นว่าตัวนี้สามารถเขียน javascript on top ได้ก็เลยสนใจครับ

## Install

ตัว zx นั้นรองรับตัว [esm](https://nodejs.org/api/esm.html) ครับทำให้เวลาใช้ต้องใช้กับ node ที่มากกว่า node v14.7 + ครับ

```bash
yarn global add zx // or npm i -g zx
```

## How to use

เผื่อเป็นการบอกว่าใช้ zx script ให้่เราทำการใส่ **shebang** บนสุดเหมือน shell script ปกติ

```javascript
// index.mjs
#!/usr/bin/env zx
```

วิธีการ run เราสามารถ run ได้ 2 ครับ

1. run script เหมือนปกติ

   ```bash
   chmod +x ./index.mjs
   ./index.mjs
   ```

2. run ผ่าน zx

   ```bash
   zx index.mjs
   ```

หลังจากนั้นเราก็เขียนเหมือน javascritp ปกติเลยครับ แต่ตัว zx มัน provide package มาให้บางตัวอยู่แล้วทำให้เราไม่จำเป็นต้อง import มาครับ ดูได้ตาม [ลิ้งนี้](https://github.com/google/zx#documentation)

**feature** คร่าวๆที่ผมชอบนะครับคือ

1. $`command`

   เราสามารถรัน command ได้ผ่านตัว $ เช่น `$`git status``

2. พวก package node พื้นฐาน เช่น os, fs, fetch

   เราสามารถใช้งาน os package ได้เลย เช่น

   ```javascript
   #!/usr/bin/env zx
   const homeDir = await os.homedir();
   ```

3. Executing remote scripts

   เราสามารถ execute script ได้ตรงๆ เวลาใช้งาน zx command ตามด้วย arg ที่ขึ้นด้วย https ลองเล่นโดยการพิมพ์

   ```bash
   zx https://cdn.jsdelivr.net/gh/jungai/zx-for-my-post/index.mjs
   ```

จากที่ได้ลองเล่นมาไม่ได้ลองทุก function ที่มัน provide ให้ครับ ผมรู้สึกว่าโอเคผมสามารถเขียน shell script ได้บ้างครับ สิ่งที่ผมเอาลองใช้ก็คร่าวๆถ้าได้ลองมากกว่านี้จะมา deep ให้ฟังกันครับผม

## Examples

- **[update dotfile](https://github.com/jungai/dotfiles/blob/master/index.mjs)**
- **[install script](https://github.com/jungai/install-linux/blob/master/index.mjs)**
