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
    <li>
        <a href="#x-bindclass">x-bind:class</a>
    </li>
    <li>
        <a href="#x-bindstyle">x-bind:style</a>
    </li>
    <li>
        <a href="#x-bindid">x-bind:id</a>
    </li>
    <li>
        <a href="#x-on">x-on</a>
    </li>
    <li>
        <a href="#x-model">x-model</a>
    </li>
    <li>
        <a href="#x-effect">x-effect</a>
    </li>
    <li>
        <a href="#x-ignore">x-ignore</a>
    </li>
    <li>
        <a href="#x-ref">x-ref</a>
    </li>
    <li>
        <a href="#tambahan">Tambahan</a>
    </li>
    <li>
        <a href="#el">$el</a>
    </li>
    <li>
        <a href="#refs--store">$refs & $store</a>
    </li>
    <li>
        <a href="#watch">$watch</a>
    </li>
    <li>
        <a href="#dispatch">$dispatch</a>
    </li>
    <li>
        <a href="#nexttick">$nextTick</a>
    </li>
    <li>
        <a href="#root">$root</a>
    </li>
    <li>
        <a href="#data">$data</a>
    </li>
    <li>
        <a href="#id--x-id">$id & x-id</a>
    </li>
  </ol>
</details>

# Tentang Repo

Repo ini saya buat sebagai riwayat sekaligus rangkuman belajar materi AlpineJS.  
Materi ini saya dapat dari berbagai sumber, tapi berpatok kepada [Video YT @TheCodeholic](https://youtu.be/5ILDMMLgX0E) karena materinya lengkap, langsung studi kasus membuat component, dan menambahkan plugin.  
Materi ini tidak termasuk challange  
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
- Nanti kalian akan menemukan kasus untuk memakan x-data dan x-init sekaligus. x-data sebagai menyimpan data, x-init bisa jadi untuk menjalankan fungsi / call API.

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
- Untuk selengkapnya, cek saja di dokumentasi [x-transition](https://alpinejs.dev/directives/transition)

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

- x-bind:class juga bisa menggunakan object syntax. Tapi sebaiknya jangan gegabah. Untuk selengkapnya, cek saja di dokumentasi [x-on#class-object-syntax](https://alpinejs.dev/directives/bind#class-object-syntax)

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

# x-on

- x-on digunakan untuk memberikan Javascript Event kedalam komponen AlpineJS
- Selengkapnya tentang Javascript Event dapat dilihat [di sini](https://developer.mozilla.org/en-US/docs/Web/API/Event)
- x-on dituliskan x-on:{javascriptEvent}. Contohnya `x-on:click=""`
- x-on dapat disingkat menjadi @. Contohnya `@click=""`
- $event digunakan untuk mengakses DOM element $this.

```html
<div x-data="{keyword:''}">
  <button @click="alert('Hello World!')">Say Hi</button>
  <label x-text="keyword"></label>
  <input type="text" @keyup.debounce="keyword = $event.target.value" />
  <div x-data="{modal: false}">
    <button @click="modal = true">Show Modal</button>
    <div x-show="modal" @click.outside="modal = false">Modal Content...</div>
  </div>
</div>
```

- AlpineJS menawarkan cara untuk kustomisasi Event dengan magic property $dispatch
- Untuk selengkapnya, cek saja di dokumentasi [$dispatch](https://alpinejs.dev/magics/dispatch)

```html
<div x-data @edit="console.log('Edit Clicked')">
  <button @click="$dispatch('edit')">Edit</button>
</div>
```

- AlpineJS menawarkan beberapa directive modifier untuk mengkustomisasi event listener seperti diantaranya `.prevent`, `.stop`, `outside`, `.window`, `.document`, `.once`, `.debounce`, `.throttle`, `.self`, `camel`, `.dot`, `.passive`, dan `.capture`
- Untuk selengkapnya, cek saja di dokumentasi [x-on#modifier](https://alpinejs.dev/directives/on#modifiers)

<p align="right"><a href="#top">Go 🔝</a></p>

# x-model

- x-model digunakan untuk mengikat value pada input element kepada x-data. Jadi kalo value pada imputan berubah, maka x-data ikut berubah, begitupun sebaliknya.
- x-model bekerja pada input element seperti `input`, `textarea`, `select`

```html
<div x-data="{keyword: null}">
  <input
    type="text"
    placeholder="Search for items"
    x-model.debounce.500ms="keyword"
  />
  <p x-text="keyword"></p>
  <button @click="keyword = null">Kosongkan</button>
</div>
```

- AlpineJS menawarkan beberapa directive modifier untuk mengkustomisasi event listener seperti diantaranya `.lazy`, `.number`, .`debounce`, `.throttle`, dan `.fill`.
- Untuk selengkapnya, cek saja di dokumentasi [x-model#modifier](https://alpinejs.dev/directives/model#modifiers)
<p align="right"><a href="#top">Go 🔝</a></p>

# x-effect

- x-effect digunakan untuk memantau state yang ada didalamnya. Jika state didalamnya berubah, maka x-effect akan diupdate.

```html
<div x-data="{name: 'Zura', message: null}">
  <p x-effect="message = 'Hello ' + name"></p>
  <p x-text="message"></p>
  <button @click="name= 'John'">Change Name</button>
</div>
```

<p align="right"><a href="#top">Go 🔝</a></p>

# x-ignore

- x-ignore digunakan untuk mengabaikan element yang terdapat pada komponen AlpineJS

```html
<div x-data="{name: 'Zura'}">
  <div x-ignore>
    <p x-text="name"></p>
  </div>
</div>
```

<p align="right"><a href="#top">Go 🔝</a></p>

# x-ref

- x-ref digunakan untuk mengakses DOM element yang lain (bukan $this)
- x-ref sebagai inisialisasi, $refs untuk akses

```html
<div x-data>
  <input x-ref="inputEmail" type="text" placeholder="Email" />
  <button @click="$refs.inputEmail.style.borderColor = 'red'">Check</button>
</div>
```

<p align="right"><a href="#top">Go 🔝</a></p>

# x-cloack

- Dalam kasus x-show yang false, kan terlihat kontennya sebentar lalu kemudian baru dihilangkan oleh AlpineJS. Untuk mengatasi ini bisa menggunakan x-cloack
- Caranya menambahkan css lalu menambahkan atribut x-cloack pada element x-show.

```css
/* CSS */
[x-cloak] {
  display: none !important;
}
```

```html
<!-- Komponen AlpineJS -->
<div x-data="{open: false}">
  <button @click="open = !open">Open/Close</button>
  <div x-show="open" x-cloak>Modal Content...</div>
</div>
```

<p align="right"><a href="#top">Go 🔝</a></p>

# x-teleport

- x-teleport digunakan untuk memindahkan element pada DOM tree
- x-teleport harus ditempatkan pada tag \<template> dan tag \<template> HARUS berisi hanya satu elemen root

```html
<div x-data>
  <p>Some Content</p>

  <div x-data="{open: false}">
    <button @click="open = !open">Open Modal</button>
    <template x-teleport="#tele">
      <div x-show="open">Modal Content</div>
    </template>
  </div>

  <p>More Content</p>
  <div id="tele">
    <p>
      Lorem ipsum dolor sit amet consectetur, adipisicing elit. Impedit,
      distinctio?
    </p>
  </div>
  <p>Lorem More Content</p>
</div>
```

<p align="right"><a href="#top">Go 🔝</a></p>

# Tambahan

- x-id akan dibahas pada magic property $id
- x-modelable tidak terbahas
- Sekarang masuk ke Magic Property `$`

<p align="right"><a href="#top">Go 🔝</a></p>

# $el

- $el digunakan untuk mengakses elemen DOM saat ini

```html
<div x-data x-init="console.log('Init ', $el)">
  <button @click="console.log($el)">Button</button>
</div>
```

<p align="right"><a href="#top">Go 🔝</a></p>

# $refs & $store

- $refs sudah dibahas pada x-ref
- $store sudah dibahas pada Data coming from store

<p align="right"><a href="#top">Go 🔝</a></p>

# $watch

- $watch digunakan untuk memantau isi state. Kita bisa memberikan fungsi ketika isi state berubah.

```html
<div
  x-data="{modal: false}"
  x-init="$watch('modal', (val) => console.log(val))"
>
  <button @click="modal = !modal">$watch example</button>
</div>
```

- $watch juga dapat mengambil isi state sebelumnya dengan menambahkan argumen kedua (optional)

```html
<div
  x-data="{modal: false}"
  x-init="$watch('modal', (val, old) => console.log(val, old))"
>
  <button @click="modal = !modal">$watch example</button>
</div>
```

- Untuk selengkapnya, cek saja di dokumentasi [$watch](https://alpinejs.dev/magics/watch)

<p align="right"><a href="#top">Go 🔝</a></p>

# $dispatch

- $dispatch sudah dibahas pada x-on

<p align="right"><a href="#top">Go 🔝</a></p>

# $nextTick

- $nextTick digunakan untuk menjalankan expresi setelah proses reactive DOM beres.

```html
<div x-data="{name: 'Zura'}">
  <button
    @click="name = 'John'; $nextTick(() => console.log($refs.p.innerText));"
  >
    Change Name
  </button>
  <p x-ref="p" x-text="name"></p>
</div>
```

<p align="right"><a href="#top">Go 🔝</a></p>

# $root

- $root digunakan untuk mengambil root element AlpineJS terdekatnya (x-data)
<p align="right"><a href="#top">Go 🔝</a></p>

```html
<div x-data id="1">
  <div>
    <div x-data id="2">
      <div>
        <button @click="console.log($root)">Button</button>
      </div>
    </div>
  </div>
</div>
```

# $data

- $data digunakan untuk mengakses Data AlpineJS pada x-data.

```html
<div x-data="dropdown">
  <div>
    <button @click="console.log($data.open)">$data</button>
  </div>
</div>
```

<p align="right"><a href="#top">Go 🔝</a></p>

# $id & x-id

- $id digunakan untuk menggenerate ID untuk setiap element agar tidak ada yang konflik.

```html
<div x-data>
  <input type="text" :id="$id('text-input')" />
  <input type="text" :id="$id('text-input')" />
</div>
```

- x-id digunakan untuk grouping scope id kalau-kalau idnya akan dipakai 2 kali / di element lain

```html
<div x-data="{ id: $id('text-input') }">
    <label :for="id">
    <input type="text" :id="id">
</div>

<div x-data="{ id: $id('text-input') }">
    <label :for="id">
    <input type="text" :id="id">
</div>
```

- Untuk selengkapnya, cek saja di dokumentasi [$id](https://alpinejs.dev/magics/id)

<p align="right"><a href="#top">Go 🔝</a></p>

# Judul

<p align="right"><a href="#top">Go 🔝</a></p>
