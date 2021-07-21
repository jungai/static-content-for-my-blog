---
name: "asdf"
title: "พามารู้จัก asdf กันครับ"
date: "2021-05-16T08:30:37.917Z"
---

## What is asdf

[asdf](https://asdf-vm.com/#/) คือ เครื่องมือที่ใช้ควบคุม runtime ของ ภาษาต่างๆ หรือ package พวก yarn เป็นต้น, ใช้งานผ่าน command line

## Background

เมื่อก่อนผมเจอปัญหาประมาณเกือบ2ปีแล้วมั้ง ปัญหาก็คือ node v13 ไม่รองรับ [nuxt](https://nuxtjs.org/) ทำให้ไม่เราสามารถ run ได้ครับ ตอนนั้นผมได้เผลอ update ไป debug อยู่นานเลยว่าเป็นเพราะอะไร 😂

หลังจากนั้นผมก็ได้ใช้ [nvm](https://github.com/nvm-sh/nvm) เป็นหลักและมันก็มี [n](https://github.com/tj/n) อีกตัวในการ manage node version ครับ ซึ่งทั้ง 2 ตัวนี้สามารถควบคุม version ได้แค่ node (ก็เนอะมันบอกอยู่ node version management) หลังจากนั้นก็ได้ยินเจ้าตัว asdf ว่ามันสามารถ manage อยากอื่นได้นอกจากตัว node ลองดูผลลัพธ์ ข้างล่าง

```
🐖 asdf list
nodejs
  12.16.1
  12.18.1
  12.18.3
  12.18.4
  14.15.4
  14.16.0
  16.0.0
pnpm
  6.0.1
  6.1.0
rust
  1.51.0
yarn
  1.22.4
```

จากที่เห็นผมมีพวก programming language กับ package ต่างๆที่บางอันมีหลายเวอร์ชั่น

## Install Asdf

ผมแนะนำให้ install ผ่านตัว git นะครับ เห็นว่ามีบางปัญหาถ้าลงผ่าน homebrew, linuxbrew

```bash
git clone https://github.com/asdf-vm/asdf.git ~/.asdf --branch v0.8.0
```

เพิ่ม script ลงไปใน shell ที่ใช้ส่วนตัวเลย (ผมใช้ zsh)

```bash
. $HOME/.asdf/asdf.sh
```

จากนั้นลองพิมพ์ `asdf`

```
🐖 asdf
version: v0.8.0-c6145d0

MANAGE PLUGINS
asdf plugin add <name> [<git-url>]      Add a plugin from the plugin repo OR,
                                        add a Git repo as a plugin by
                                        specifying the name and repo url
asdf plugin list [--urls] [--refs]      List installed plugins. Optionally show
                                        git urls and git-ref
asdf plugin list all                    List plugins registered on asdf-plugins
                                        repository with URLs
asdf plugin remove <name>               Remove plugin and package versions
	.....
```

เป็นการติดตั้งตัว asdf เสร็จสิ้น...... เดี๋ยวก่อน อันนี้คือแค่เริ่มต้นครับ เรายังไม่ได้ install พวก ภาษาหรือ package เลย

## Install Plugins

หลังจากที่ติดตั้งตัว asdf แล้ว เราต้องติดตั้งตัว asdf plugin โดยดูได้จาก [ลิ้งนี้](https://asdf-vm.com/#/plugins-all) ครับ โดยตัวอย่างผมจะ install plugin nodejs (แน่นอนผมเขียนเป็นแค่ javascript😢)
โดยใช้ command -> `asdf plugin add <plugin_name>`

- **note**

  - เราควรลบ package ที่ติดตั้งไปก่อนหน้านี้ก่อนนะครับเพื่อกันไม่ให่เกิด conflict (ที่ไม่ได้ติดตั้งจาก asdf เช่น nodejs ถ้าเรา install ผ่านตัว homebrew)
  - ถ้าเราจะติดตั้ง nodejs เราต้อง install ตาม [requirement](https://github.com/asdf-vm/asdf-nodejs) บางอย่างก่อนนะครับ ซึ่งบาง plugin ก็ไม่มี requirement ครับดูได้ตาม ลิ้งข้างบน

สมมติว่าเราต้องติดตั้งตาม requirement แล้วก็ลุยยยย

```bash
asdf plugin add nodejs
```

ก็จะได้

```
🐖 asdf plugin list
nodejs
```

## Management Version

ทีนี้เมื่อเราติดตั้ง plugin แล้วก็เลือกเวอร์ชั่นที่เราต้องการได้เลย อย่างเช่นตัวอย่างผมติดตั้ง plugin nodejs ผมอยากจะติดตั้ง node v16

```bash
asdf install nodejs 16.0.0
```

หรือถ้าอยากได้เวอร์ชั่นล่าสุด

```bash
asdf install nodejs latest
```

หลังจากนั้น ลองพิมพ์ `asdf list` จะโชว์ plugin ที่เรามี + version ต่างๆ ลองพิมพ์ `node -v` มันจะแจ้งว่าไม่มี node ถูก set เอาไว้ อ่าว..... แล้วที่เรา install ไปละ ?

เป็นเพราะว่าเราไม่ได้ set global เอาไว้นั้นเองมันเลยหา node ไม่เจอ ถ้าต้องการจะ set global พิมพ์ `asdf global <plugin|package> <version>`

```bash
asdf global nodejs 16.0.0
```

หลังจากนั้นลองพิมพ์ `node -v` ใหม่ก็ขึ้น node ที่เรา set ไว้ครับ

## Tips

ในทุกๆ project เราอาจจะใช้ node version ที่ต่างกันเช่น proj1 ใช้ node12, proj2 ใช้ node 10 อะไรแบบนี้

เพื่อเป็นการบอกเราว่าโปรเจคนี้ใช้ node เวอร์ชั่นไหน ให้เราทำการสร้างไฟล์ที่ชื่อว่า **.tool-versions**

```
// .tool-version
nodejs 16.0.0
```

เวลาเราจะ install หรือ run command มันจะแจ้งเตือนเราว่า node ไม่ตรงกับ project นี้ให้ทำการ install node version ของตัว project ครับผม

## ​Summary

asdf เป็น tool ตัวหนึ่งที่ผมเห็นว่าดีมากๆครับ อยากจะให้ลองใช้กันดูครับ คิดว่าน่าจะช่วยแก้ปัญหา node version ไม่ตรง run แล้วเกิด bug ครับ
