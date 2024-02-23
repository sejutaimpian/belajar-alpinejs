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
    <li>
        <a href="#intro-masuk-komponen">Intro masuk komponen</a>
    </li>
    <li>
        <a href="#dropdown">Dropdown</a>
    </li>
    <li>
        <a href="#modal">Modal</a>
    </li>
    <li>
        <a href="#tabs">Tabs</a>
    </li>
    <li>
        <a href="#carousel">Carousel</a>
    </li>
    <li>
        <a href="#accordion">Accordion</a>
    </li>
    <li>
        <a href="#notification">Notification</a>
    </li>
    <li>
        <a href="#popover">Popover</a>
    </li>
    <li>
        <a href="#intro-masuk-plugin">Intro masuk plugin</a>
    </li>
    <li>
        <a href="#mask">Mask</a>
    </li>
    <li>
        <a href="#intersect">Intersect</a>
    </li>
    <li>
        <a href="#persist">Persist</a>
    </li>
    <li>
        <a href="#focus">Focus</a>
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

- Jika kamu menggunakan vscode, sebaiknya instal extensions [Alpine.js IntelliSense](https://marketplace.visualstudio.com/items?itemName=adrianwilczynski.alpine-js-intellisense) dan [alpine-syntax-highlight](https://marketplace.visualstudio.com/items?itemName=sperovita.alpinejs-syntax-highlight) untuk mempermudah dan menjadikan belajar AlpineJS menyenangkan

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
// File app.js
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
<!-- Menghubungkan ke file app.js -->
<script src="app.js"></script>
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
// app.js
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
- Nanti kalian akan menemukan kasus untuk memakai x-data dan x-init sekaligus. x-data sebagai menyimpan data, x-init bisa jadi untuk menjalankan fungsi / call API.

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

```html
<div
  x-data="{
        open: false,
        get isOpen() {
            return this.open;
        },
        set isOpen(open) {
            this.open = open
        },
        toggle(){
          this.isOpen = !this.isOpen
        }
    }"
>
  <button @click="toggle()">Open/Close</button>
  <div x-show="isOpen">Content</div>
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

# Intro masuk komponen

- TheCodeholic membuat folder tersendiri untuk materi komponen.
- TheCodeholic tetap membuat file app.js namun pada kenyataannya tidak digunakan. Jadi sebaiknya jangan ditiru.
- Install TailwindCSS untuk mempercantik tampilan komponen. Boleh menggunakan CDN untuk pembelajaran.
- Jika kamu menggunakan vscode, sebaiknya instal ekstensions [Tailwind CSS IntelliSense](https://marketplace.visualstudio.com/items?itemName=bradlc.vscode-tailwindcss)
- Jika kamu menggunakan TailwindCSS via CDN, sebaiknya membuat file `tailwind.config.js` dengan tanpa isi, jadi hanya membuat file saja dan tidak bekerja disana. langkah dimaksudkan untuk mengaktifkan fitur dari ekstensions [Tailwind CSS IntelliSense](https://marketplace.visualstudio.com/items?itemName=bradlc.vscode-tailwindcss)

<p align="right"><a href="#top">Go 🔝</a></p>

# Dropdown

- x-data="{open: false}"
- @click="open = !open"
- :class="{'rotate-90': open}
- x-show="open"
- @click.outside="open = false"
- x-transition

```html
<div x-data="{open: false}">
  <button
    @click="open = !open"
    class="inline-flex items-center py-2 px-6 bg-purple-600 hover:bg-opacity-95 text-white rounded-md shadow"
  >
    Toggle
    <svg
      xmlns="http://www.w3.org/2000/svg"
      class="h-4 w-4 ml-2 transition-all"
      :class="{'rotate-90': open}"
      fill="none"
      viewBox="0 0 24 24"
      stroke="currentColor"
      stroke-width="2"
    >
      <path stroke-linecap="round" stroke-linejoin="round" d="M9 5l7 7-7 7" />
    </svg>
  </button>
  <ul
    x-show="open"
    @click.outside="open = false"
    x-transition
    class="absolute bg-white w-[160px] shadow-md py-1"
  >
    <li>
      <a class="py-1 px-2 hover:bg-gray-200 flex items-center" href="#">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-4 w-4 mr-2"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
          stroke-width="2"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"
          />
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z"
          />
        </svg>
        Open
      </a>
    </li>
    <li>
      <a class="py-1 px-2 hover:bg-gray-200 flex items-center" href="#">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-4 w-4 mr-2"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
          stroke-width="2"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z"
          />
        </svg>
        Edit
      </a>
    </li>
    <li>
      <a class="py-1 px-2 hover:bg-gray-200 flex items-center" href="#">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-4 w-4 mr-2"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
          stroke-width="2"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"
          />
        </svg>
        Delete
      </a>
    </li>
  </ul>
</div>
```

<p align="right"><a href="#top">Go 🔝</a></p>

# Modal

- x-data="{open: false, accept() {console.log('accepted')}}"
- @click="open = true"
- \<template x-teleport="body">
- x-show="open"
- x-transition
- @click.outside="open = false"
- @click="open = false"
- @click="accept"

```html
<div
  x-data="{
        open: false, 
        accept() {console.log('accepted')}
    }"
>
  <button
    @click="open = true"
    class="inline-flex items-center py-2 px-6 bg-purple-600 hover:bg-opacity-95 text-white rounded-md shadow"
  >
    Toggle Modal
  </button>
  <template x-teleport="body">
    <!-- Backdrop -->
    <div
      x-show="open"
      class="fixed flex justify-center items-center left-0 top-0 bottom-0 right-0 z-10 bg-black/50"
    >
      <!-- Dialog -->
      <div
        x-show="open"
        x-transition
        @click.outside="open = false"
        class="w-[90%] md:w-1/2 bg-white rounded-lg"
      >
        <!-- Modal Title -->
        <div
          class="py-2 px-4 text-lg font-semibold bg-gray-100 rounded-t-lg flex items-center justify-between"
        >
          <h2>Modal Title</h2>
          <button @click="open = false">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="h-6 w-6"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor"
              stroke-width="2"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="M6 18L18 6M6 6l12 12"
              />
            </svg>
          </button>
        </div>
        <!-- Modal Body -->
        <div class="p-4">Modal Content</div>
        <!-- Modal Footer -->
        <div
          class="py-2 px-4 text-lg flex justify-end font-semibold bg-gray-100 rounded-b-lg"
        >
          <button
            @click="accept"
            class="inline-flex items-center py-1 px-3 bg-emerald-500 hover:bg-opacity-95 text-white rounded-md shadow mr-2"
          >
            Accept
          </button>
          <button
            @click="open = false"
            class="inline-flex items-center py-1 px-3 bg-gray-300 hover:bg-opacity-95 text-gray-800 rounded-md shadow"
          >
            Cancel
          </button>
        </div>
      </div>
    </div>
  </template>
</div>
```

<p align="right"><a href="#top">Go 🔝</a></p>

# Tabs

- x-data="{  
  tabs: ['Home', 'Users', 'Settings', 'Orders'],  
  activeTab: 'Home'  
  }"
- x-for="tab in tabs"
- @click="activeTab = tab"
- x-text="tab"
- :class="{'border-purple-500': activeTab === tab, 'text-blue-500': activeTab === tab}"
- x-show="activeTab === 'Home'"
- x-show="activeTab === 'Users'"
- x-show="activeTab === 'Settings'"
- x-show="activeTab === 'Orders'"
- x-transition

```html
<div
  x-data="{
        tabs: ['Home', 'Users', 'Settings', 'Orders'],
        activeTab: 'Home'
    }"
>
  <div class="flex">
    <template x-for="tab in tabs">
      <a
        @click="activeTab = tab"
        x-text="tab"
        class="py-2 px-3 bg-white cursor-pointer border"
        :class="{'border-purple-500': activeTab === tab, 'text-blue-500': activeTab === tab}"
      ></a>
    </template>
  </div>
  <div class="py-2 px-3 bg-white border">
    <!-- Home -->
    <div x-show="activeTab === 'Home'" x-transition>Home</div>
    <!-- Users -->
    <div x-show="activeTab === 'Users'" x-transition>Users</div>
    <!-- Settings -->
    <div x-show="activeTab === 'Settings'" x-transition>Settings</div>
    <!-- Orders -->
    <div x-show="activeTab === 'Orders'" x-transition>Orders</div>
  </div>
</div>
```

<p align="right"><a href="#top">Go 🔝</a></p>

# Carousel

- Khusus komponen ini mengharuskan download gambar.

```html
<div
  x-data="{
  images: ['img/1.jpg', 'img/2.jpg', 'img/3.jpg', 'img/4.jpg'],
  activeImage: null,
  prev() {
      let index = this.images.indexOf(this.activeImage);
      if (index === 0) 
          index = this.images.length;
      this.activeImage = this.images[index - 1];
  },
  next() {
      let index = this.images.indexOf(this.activeImage);
      if (index === this.images.length - 1) 
          index = -1;
      this.activeImage = this.images[index + 1];
  },
  init() {
      this.activeImage = this.images.length > 0 ? this.images[0] : null
  }
}"
>
  <div class="relative">
    <template x-for="image in images">
      <div
        x-show="activeImage === image"
        x-transition
        class="aspect-w-3 aspect-h-2"
      >
        <img :src="image" alt="" class="object-cover" />
      </div>
    </template>
    <a
      @click.prevent="prev"
      class="cursor-pointer text-white absolute left-0 top-1/2 -translate-y-1/2"
    >
      <svg
        xmlns="http://www.w3.org/2000/svg"
        class="h-10 w-10"
        fill="none"
        viewBox="0 0 24 24"
        stroke="currentColor"
        stroke-width="2"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          d="M15 19l-7-7 7-7"
        />
      </svg>
    </a>
    <a
      @click.prevent="next"
      class="cursor-pointer text-white absolute right-0 top-1/2 -translate-y-1/2"
    >
      <svg
        xmlns="http://www.w3.org/2000/svg"
        class="h-10 w-10"
        fill="none"
        viewBox="0 0 24 24"
        stroke="currentColor"
        stroke-width="2"
      >
        <path stroke-linecap="round" stroke-linejoin="round" d="M9 5l7 7-7 7" />
      </svg>
    </a>
  </div>
  <div class="flex">
    <template x-for="image in images">
      <a
        @click="activeImage = image"
        class="cursor-pointer w-[80px] border border-gray-300 hover:border-purple-500 flex items-center justify-center"
        :class="{'border-purple-600': activeImage === image}"
      >
        <img :src="image" alt="" class="object-cover" />
      </a>
    </template>
  </div>
</div>
```

<p align="right"><a href="#top">Go 🔝</a></p>

# Accordion

- x-data="{
  items: [
  {title: 'Item 1', body: 'Body 1'},
  {title: 'Item 2', body: 'Body 2'},
  {title: 'Item 3', body: 'Body 3'},
  {title: 'Item 4', body: 'Body 4'},
  ],
  activeItem: null,
  selectItem(item) {
  if (this.activeItem === item) {
  this.activeItem = null
  } else {
  this.activeItem = item
  }
  }
  }"
- x-for="item in items"
- @click="selectItem(item)"
- x-text="item.title"
- :class="{'rotate-90': activeItem === item}"
- x-show="activeItem === item"
- x-transition
- x-html="item.body"

```html
<div
  x-data="{
        items: [
            {title: 'Item 1', body: 'Body 1'},
            {title: 'Item 2', body: 'Body 2'},
            {title: 'Item 3', body: 'Body 3'},
            {title: 'Item 4', body: 'Body 4'},
        ],
        activeItem: null,
        selectItem(item) {
            if (this.activeItem === item) {
                this.activeItem = null
            } else {
                this.activeItem = item
            }
        }
    }"
>
  <template x-for="item in items">
    <div>
      <div
        @click="selectItem(item)"
        class="py-1 px-2 bg-gray-50 border cursor-pointer hover:text-blue-400 transition-all font-semibold flex justify-between items-center"
      >
        <span x-text="item.title"></span>
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-4 w-4 transition-all"
          :class="{'rotate-90': activeItem === item}"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
          stroke-width="2"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            d="M9 5l7 7-7 7"
          />
        </svg>
      </div>
      <div
        x-show="activeItem === item"
        x-transition
        x-html="item.body"
        class="p-2 bg-white border"
      ></div>
    </div>
  </template>
</div>
```

<p align="right"><a href="#top">Go 🔝</a></p>

# Notification

```html
<div
  x-data="{
  visible: true,
  timeout: 5000,
  percent: 0,
  interval: null,
  close() {
      this.visible = false;
      clearInterval(this.interval)
  },
  init() {
      setTimeout(() => {
         this.visible = false;
      }, this.timeout)
      const startDate = Date.now();
      const futureDate = Date.now() + this.timeout;
      this.interval = setInterval(() => {
          const date = Date.now();
          this.percent = (date - startDate) * 100 / (futureDate - startDate);
          if (this.percent >= 100) {
              clearInterval(this.interval)
          }
      }, 30)
  }
}"
  x-show="visible"
  class="relative py-2 px-4 pb-4 bg-emerald-500 text-white"
>
  <div class="font-semibold mb-2">Lorem ipsum dolor sit</div>
  <div class="text-sm">
    Lorem ipsum dolor sit, amet consectetur adipisicing elit. Porro ea placeat
    sed soluta velit sint, adipisci consequuntur quaerat alias consectetur iste
    perspiciatis ducimus consequatur vitae? Officia, assumenda. Nobis, expedita
    optio.
  </div>
  <button
    @click="close"
    class="absolute flex items-center justify-center right-2 top-2 w-[30px] h-[30px] rounded-full hover:bg-black/10 transition-colors"
  >
    <svg
      xmlns="http://www.w3.org/2000/svg"
      class="h-6 w-6"
      fill="none"
      viewBox="0 0 24 24"
      stroke="currentColor"
      stroke-width="2"
    >
      <path
        stroke-linecap="round"
        stroke-linejoin="round"
        d="M6 18L18 6M6 6l12 12"
      />
    </svg>
  </button>
  <!-- Progress -->
  <div>
    <div
      class="absolute left-0 bottom-0 right-0 h-[6px] bg-black/10"
      :style="{'width': `${percent}%`}"
    ></div>
  </div>
</div>
```

<p align="right"><a href="#top">Go 🔝</a></p>

# Popover

```html
<div
  x-data="{
  show: false, 
  title: 'Test Popover',
  message: 'Test <b>popover</b> message',
  showPopover() {
      console.log(this.$refs.button, this.$refs.popover)
      this.show = !this.show
  }
}"
  class="relative flex justify-center"
>
  <button
    x-ref="button"
    @click="showPopover"
    class="inline-flex items-center py-2 px-6 bg-purple-600 hover:bg-opacity-95 text-white rounded-md shadow"
  >
    Popover
  </button>
  <div
    x-ref="popover"
    x-show="show"
    x-transition
    class="absolute mb-2 bottom-[100%] shadow-lg bg-white w-[200px] rounded"
  >
    <!-- Header -->
    <div class="flex justify-between items-center font-semibold py-1 px-2">
      <span x-text="title"></span>
      <svg
        xmlns="http://www.w3.org/2000/svg"
        class="h-4 w-4"
        fill="none"
        viewBox="0 0 24 24"
        stroke="currentColor"
        stroke-width="2"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          d="M6 18L18 6M6 6l12 12"
        />
      </svg>
    </div>
    <!-- Body -->
    <div x-html="message" class="p-3 text-sm"></div>
  </div>
</div>
```

<p align="right"><a href="#top">Go 🔝</a></p>

# Intro masuk plugin

- Pastikan untuk menempatkan cdn plugin diatas cdn alpine core

<p align="right"><a href="#top">Go 🔝</a></p>

# Mask

- Mask digunakan untuk memformat inputan user otomatis & dinamis. contohnya nomor hp, kartu kredit, dll
- Instalasi bisa menggunakan CDN.
- Pastikan untuk menempatkan cdn plugin diatas cdn alpine core

```html
<!-- Alpine Mask Plugins -->
<script
  defer
  src="https://cdn.jsdelivr.net/npm/@alpinejs/mask@3.x.x/dist/cdn.min.js"
></script>

<!-- Alpine Core -->
<script
  defer
  src="https://cdn.jsdelivr.net/npm/alpinejs@3.12.1/dist/cdn.min.js"
></script>
```

- Mask directive menggunakan `x-mask`

```html
<div x-data>
  <input type="text" x-mask="99/99/9999" placeholder="MM/DD/YYYY" />

  <input
    x-mask:dynamic="
      $input.startsWith('34') || $input.startsWith('37')
          ? '9999 999999 99999' : '9999 9999 9999 9999'
  "
  />
</div>
```

<p align="right"><a href="#top">Go 🔝</a></p>

# Intersect

- Intersect digunakan untuk mengatur element saat berada di viewport.
- Berguna untuk lazy load images/content, triggering animations, dll
- Untuk coding pugin ini menggunakan TailwindCSS
- Instalasi bisa menggunakan CDN.
- Pastikan untuk menempatkan cdn plugin diatas cdn alpine core

```html
<!-- Alpine Plugins -->
<script
  defer
  src="https://cdn.jsdelivr.net/npm/@alpinejs/intersect@3.x.x/dist/cdn.min.js"
></script>
<!-- Alpine Core -->
<script
  defer
  src="https://cdn.jsdelivr.net/npm/alpinejs@3.12.1/dist/cdn.min.js"
></script>
```

- Intersect directive menggunakan `x-intersect`

```html
<div class="bg-gray-800 min-h-screen text-white">null</div>
<div x-data="{ shown: false }" x-intersect="shown = true">
  <div x-show="shown" x-transition>I'm in the viewport!</div>
</div>
<div x-data>
  <div
    x-data="{dataSrc: '1.jpg', src: null}"
    class="w-48 h-48 border"
    x-intersect.once.half="src = dataSrc"
  >
    <img x-show="src" x-transition :src="src" alt="" />
  </div>
</div>
<div class="bg-gray-800 min-h-screen text-white">null</div>
```

<p align="right"><a href="#top">Go 🔝</a></p>

# Persist

- Persist digunakan untuk menyimpan state ke localStorage.
- Instalasi bisa menggunakan CDN.
- Pastikan untuk menempatkan cdn plugin diatas cdn alpine core

```html
<!-- Alpine Plugins -->
<script
  defer
  src="https://cdn.jsdelivr.net/npm/@alpinejs/persist@3.x.x/dist/cdn.min.js"
></script>
<!-- Alpine Core -->
<script
  defer
  src="https://cdn.jsdelivr.net/npm/alpinejs@3.12.1/dist/cdn.min.js"
></script>
```

- Persist menggunakan magic method `$persist`

```html
<div x-data="{count: $persist(0).as('my-count').using(localStorage)}">
  <button
    x-on:click="count++"
    class="inline-flex items-center py-2 px-6 bg-purple-600 hover:bg-opacity-95 text-white rounded-md shadow"
  >
    Increment
  </button>

  <span x-text="count"></span>
</div>
```

- Untuk selengkapnya, cek saja di dokumentasi [Persist](https://alpinejs.dev/plugins/persist)

<p align="right"><a href="#top">Go 🔝</a></p>

# Focus

- Focus digunakan untuk memanage focus element untuk keperluan `tab`
- Instalasi bisa menggunakan CDN.
- Pastikan untuk menempatkan cdn plugin diatas cdn alpine core

```html
<!-- Alpine Plugins -->
<script
  defer
  src="https://cdn.jsdelivr.net/npm/@alpinejs/focus@3.x.x/dist/cdn.min.js"
></script>
<!-- Alpine Core -->
<script
  defer
  src="https://cdn.jsdelivr.net/npm/alpinejs@3.12.1/dist/cdn.min.js"
></script>
```

- Focus directive menggunakan `x-trap`

```html
<div x-data="{ open: false }">
  <button @click="open = !open">Open Dialog</button>

  <span x-show="open" x-trap="open">
    <p>...</p>

    <input type="text" placeholder="Some input..." />

    <input type="text" placeholder="Some other input..." />

    <button @click="open = false">Close Dialog</button>
  </span>
</div>
```

- Untuk selengkapnya, cek saja di dokumentasi [Focus](https://alpinejs.dev/plugins/focus)

<p align="right"><a href="#top">Go 🔝</a></p>

# Collapse

- Collapse digunakan untuk memberikan fungsional collapse beserta animasinya.
- Instalasi bisa menggunakan CDN.
- Pastikan untuk menempatkan cdn plugin diatas cdn alpine core

```html
<!-- Alpine Plugins -->
<script
  defer
  src="https://cdn.jsdelivr.net/npm/@alpinejs/collapse@3.x.x/dist/cdn.min.js"
></script>
<!-- Alpine Core -->
<script
  defer
  src="https://cdn.jsdelivr.net/npm/alpinejs@3.12.1/dist/cdn.min.js"
></script>
```

- Collapse directive menggunakan `x-collapse`

```html
<div x-data="{ expanded: false }" class="w-1/3 mx-auto">
  <p x-show="expanded" x-collapse.min.50px>
    Lorem ipsum dolor sit amet consectetur adipisicing elit. Tempore sunt magnam
    quibusdam dignissimos excepturi quisquam repellat culpa quod cupiditate et
    animi fugit pariatur repellendus rem ratione totam, dolor voluptatem omnis.
  </p>
  <button
    @click="expanded = ! expanded"
    x-text="expanded ? 'Read Less' : 'Read More'"
  ></button>
</div>
```

<p align="right"><a href="#top">Go 🔝</a></p>

# Morph

- Saya kehabisan energi disini (gapaham)

<p align="right"><a href="#top">Go 🔝</a></p>
