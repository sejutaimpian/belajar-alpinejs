<details id="top">
  <summary>Daftar Isi</summary>
  <ol>
    <li>
        <a href="#tentang-repo">Tentang Repo</a>
    </li>
    <li>
        <a href="#introduction">Introduction</a>
    </li>
    <li>
        <a href="#installation">Installation</a>
    </li>
    <li>
        <a href="#x-data-x-text-x-html">x-data, x-text, x-html</a>
    </li>
    <li>
        <a href="#re-usable-data">Re-usable Data</a>
    </li>
    <li>
        <a href="#data-less-components">Data-Less Components</a>
    </li>
    <li>
        <a href="#data-coming-from-store">Data coming from Store</a>
    </li>
    <li>
        <a href="#x-init">x-init</a>
    </li>
    <li>
        <a href="#scoping">Scoping</a>
    </li>
    <li>
        <a href="#getter--setter">Getter & Setter</a>
    </li>
    <li>
        <a href="#x-show--x-transition">x-show & x-transition</a>
    </li>
    <li>
        <a href="#x-if">x-if</a>
    </li>
    <li>
        <a href="#x-for">x-for</a>
    </li>
    <li>
        <a href="#x-for-in-range">x-for in range</a>
    </li>
  </ol>
</details>

# Tentang Repo

Repo ini saya buat sebagai riwayat sekaligus rangkuman belajar materi AlpineJS.  
Materi ini saya dapat dari berbagai sumber, tapi berpatok kepada [Video YT @TheCodeholic](https://youtu.be/5ILDMMLgX0E) karena materinya lengkap, langsung studi kasus membuat component, dan menambahkan plugin.  
Versi AlpineJS yang saya gunakan adalah versi 3.12.1

# Introduction

> Your new, lightweight, JavaScript framework

- Kalo kata dosen kita semua (Pak Sandhika Galih), AlpineJS adalah TailwindCSS versi Javascript. Jadi kita menuliskan kode javascript langsung di file html, lebih tepatnya sebagai atribut tag html.
- Materi AlpineJS dibagi kedalam 3 bagian, yaitu materi dasar (Directive & Magic Property), materi component, dan materi plugin

<p align="right"><a href="#top">Go 🔝</a></p>

# Installation

- Ada 2 cara untuk mengintal AlpineJS, yaitu dengan cara NPM dan menggunakan CDN
- Cara yang paling mudah dan diterapkan pada video yaitu dengan CDN
- link CDN ada 2 cara juga, yaitu yang versinya diakhiri x.x (versi terbaru) atau langsung dituliskan versinya.
- Sebaiknya menggunakan cara yang langsung dituliskan versinya, karena takutnya ada fitur yang deprecated atau sebagainya.

```js
<script
  defer
  src="https://cdn.jsdelivr.net/npm/alpinejs@3.12.1/dist/cdn.min.js"
></script>
```

> Don't forget the "defer" attribute in the \<script> tag.

# x-data, x-text, x-html

- Untuk membuat component AlpineJS, kita cukup menambahkan atribut x-data kedalam tag html

```html
<div x-data>Ini adalah component AlpineJS</div>
```

- x-data juga dapat digunakan untuk menampung variable/state (variable yang reactive).

```html
<div x-data="{name: 'Zura'}">Ini adalah component AlpineJS</div>
```

- x-data juga dapat digunakan untuk menampung method

```html
<div
  x-data="{message: 'Click me to change', change(){ this.message = 'Change message' } }"
>
  <span x-html="message" @click="change()"></span>
</div>
```

- x-text digunakan untuk menampilkan state/variable pada x-data secara reactive.
- jika x-text berisi format text selain string (seperti tag html, object, array, json, dll), maka data yang ditampilkan akan berupa hardcode (diconvert ke string dan tidak mengikuti aturan html jika html)

```html
<div x-data="{name: 'Zura'}">
  <p x-text="name"></p>
</div>
```

- x-text juga dapat digunakan untuk menampilkan data dari API

```html
<div
  x-data
  x-text="await (await fetch('https://jsonplaceholder.typicode.com/todos/1')).text()"
></div>
```

- x-html memiliki kegunaan seperti x-text, tapi lebih spesifik untuk menampilkan state yang berisi tag html.

```html
<div x-data="{message: 'Hello <b>World</b>'}">
  <p x-html="message"></p>
</div>
```

# Re-usable Data

- Reusable data merupakan teknik untuk tidak mengulang-ulang membuat x-data dengan value yang sama, dengan cara memindahkan x-data ke Alpine.data
- Alpine.data merupakan bagian dari Global method.
- Alpine.data digunakan untuk reusable data
- Contoh kasus yang sering ditemukan adalah dropdown.

```html
<!-- Before -->
<div
  x-data="{
    open:false,
    toggle(){
        this.open = !this.open
    }
}"
>
  <button @click="toggle">Open/Close</button>
  <div x-show="open" x-text="message"></div>
</div>
```

- Alpine.data tidak ditempatkan di tag html, tapi di tag script. Jadi untuk membuat Alpine.data, bisa dengan cara menambahkan tag script, atau membuat file js baru lalu dihubungkan kedalam html.

```js
// File alpine.js
document.addEventListener("alpine:init", () => {
  Alpine.data("dropdown", () => ({
    open: false,
    message: "Something",

    toggle() {
      this.open = !this.open;
    },
  }));
});
```

```html
<!-- Menghubungkan ke file alpine.js -->
<script src="alpine.js"></script>
<!-- After -->
<div x-data="dropdown">
  <button @click="toggle">Open/Close</button>
  <div x-show="open" x-text="message"></div>
</div>
```

<p align="right"><a href="#top">Go 🔝</a></p>

# Data-Less Components

- Data-less components artinya component alpine yang tidak memiliki data didalamnya.
- Data-less components digunakan untuk inisialisasi component alpine kemudian memanfaatkan fitur alpine

```html
<div x-data @click="console.log('Something')">Munculkan console Something</div>
```

<p align="right"><a href="#top">Go 🔝</a></p>

# Data coming from Store

- Data cpming from Store memanfaatkan Global Method Alpine.store
- Alpine.store digunakan untuk mendeklarasikan data agar dapat diakses pada global scope (di semua tempat)
- Alpine.store tidak ditempatkan di tag html, tapi di tag script. Jadi untuk membuat Alpine.store, bisa dengan cara menambahkan tag script, atau membuat file js baru lalu dihubungkan kedalam html.

```js
// alpine.js
Alpine.store("currentUser", {
  username: "TheCodeholic",
  posts: ["Post1", "Post2"],
});
```

- Untuk mengakses data yang terdapat pada Alpine.store menggunakan `$store`

```html
<div x-data x-text="$store.currentUser.username"></div>
```

<p align="right"><a href="#top">Go 🔝</a></p>

# x-init

- x-init digunakan untuk menginisialisasi component AlpineJS.
- yang membedakan inisialisasi x-init dengan x-data adalah x-init akan langsung menjalankan perintah didalamnya.

```html
<div x-init="console.log('Init')"></div>
```

- x-data juga bisa langsung menjalankan perintah, tapi harus menggunakan function init.

```html
<div
  x-data="{
        init(){
            console.log('I am initialized')
        }
    }"
></div>
```

- x-init juga dapat digunakan untuk fetch json lalu menampilkan data tersebut pada component alpine yang sama.

```html
<div
  x-data="{todo: {}}"
  x-init="todo = await (await fetch('https://jsonplaceholder.typicode.com/todos/1')).json()"
>
  <span x-text="todo.title"></span>
</div>
```

<p align="right"><a href="#top">Go 🔝</a></p>

# Scoping

- Scoping AlpineJS akan mencari parent terdekatnya untuk mengambil variable, jika tidak ada akan terus menelusuri parentnya.

<p align="right"><a href="#top">Go 🔝</a></p>

# Getter & Setter

- Konsep getter & setter sama seperti pada javascript.
- Saya juga kurang faham soal ini, TheCodeholic juga ga terlalu menjelaskan detail.
- TheCodeholic sepertinya salah dalam penerapan getter & setter. Saya memperbaikinya di block code

```html
<div
  x-data="{
        open: false,
        get getOpen() {
            return this.open;
        },
        set setOpen(open) {
            this.open = open
        }
    }"
>
  <button @click="setOpen = !getOpen">Open/Close</button>
  <div x-show="getOpen">Content</div>
</div>
```

<p align="right"><a href="#top">Go 🔝</a></p>

# x-show & x-transition

- x-show digunakan untuk menampilkan atau menyembunyikan componen AlpineJS
- x-show menerima value boolean, true atau false.
- jika x-show bernilai true, maka AlpineJS menambahkan CSS `display:none`.

```html
<div x-data="{open: false}">
  <button @click="open = !open">Open/Close</button>
  <div x-show="open">Content...</div>
</div>
```

- x-transition digunakan untuk memberikan transition pada componen AlpineJS yang beratribut x-show

```html
<div x-data="{open: false}">
  <button @click="open = !open">Open/Close</button>
  <div x-show="open" x-transition>Content</div>
</div>
```

- x-transition bisa dikustomisasi mulai dari `duration`, `delay`, `opacity`, hingga `scale`

```html
<div x-data="{ open: false }">
  <button x-on:click="open = ! open">Open/Close</button>
  <div
    x-show="open"
    x-transition:enter.duration.200ms
    x-transition:leave.duration.2000ms
  >
    Content
  </div>
</div>
```

- Untuk selengkapnya, cek saja di dokumentasi

<p align="right"><a href="#top">Go 🔝</a></p>

# x-if

- x-if mirip seperti x-show, hanya saja x-if tidak bisa menambahkan x-transition dan dibungkus dengan tag \<template>
- x-if harus ditempatkan pada tag \<template> dan tag \<template> HARUS berisi hanya satu elemen root

```html
<div x-data="{ open: false }">
  <button x-on:click="open = ! open">Open/Close</button>
  <template x-if="open">
    <div>Content</div>
  </template>
</div>
```

<p align="right"><a href="#top">Go 🔝</a></p>

# x-for

- x-for digunakan untuk melakukan iterasi sebagaimana for di javascript
- x-for harus ditempatkan pada tag \<template> dan tag \<template> HARUS berisi hanya satu elemen root
- x-for sebaiknya memiliki :key untuk keperluan re-ordering

```html
<div x-data="{posts: [{id: 1, title: 'title 1'}, {id: 2, title: 'title 2'}]}">
  <template x-for="(post, index) in posts" :key="post.id">
    <h2 x-text="post.id + '. ' + post.title"></h2>
  </template>
</div>
```

<p align="right"><a href="#top">Go 🔝</a></p>

# x-for in range

- x-for in range artinya melakukan pengulangan langsung tanpa menggunakan bantuan total array/object.

```html
<div x-data>
  <template x-for="n in 10">
    <p x-text="n"></p>
  </template>
</div>
```

<p align="right"><a href="#top">Go 🔝</a></p>

# x-bind:class

- x-bind digunakan untuk mengatur atribut html seperti id, placeholder, class, style, dll
- untuk memudahkan kondisional, gunakanlah seperti pada javascript (Logical Operator, ternary operator, dsb)
- x-bind untuk class ditulis `x-bind:class`. x-bind untuk placeholder ditulis `x-bind:placeholder`, dst.
- x-bind mempunyai shorthand. x-bind:class menjadi `:class`, x-bind:placeholder menjadi `:placeholder`, dst
- x-bind:class memiliki kelebihan yaitu akan menambahkan class baru dan tidak menimpanya. berbeda dengan x-bind atribut yang lain, yang mana akan menimpanya.

```html
<style>
  .yellow {
    background-color: yellow;
  }

  .bordered {
    border: 2px solid brown;
  }
</style>
<div x-data="{clicked: false}">
  <button
    class="bordered"
    x-bind:class="clicked ? 'yellow' : ''"
    @click="clicked = !clicked"
  >
    Click me
  </button>
</div>
```

- x-bind:class juga bisa menggunakan object syntax. Tapi sebaiknya jangan gegabah. Untuk selengkapnya, cek saja di dokumentasi

<p align="right"><a href="#top">Go 🔝</a></p>

# x-bind:style

```html
<div x-data="{clicked: false}">
  <button
    :style="clicked && {'backgroundColor': 'red'}"
    @click="clicked = !clicked"
  >
    Click me
  </button>
</div>
```

<p align="right"><a href="#top">Go 🔝</a></p>

# x-bind:id

```html
<button
  x-data="{id: ''}"
  x-bind:id="id"
  @click="id = Math.round(Math.random() * 10000)"
>
  Random id = <span x-text="id"></span>
</button>
```

<p align="right"><a href="#top">Go 🔝</a></p>

# Judul

<p align="right"><a href="#top">Go 🔝</a></p>
