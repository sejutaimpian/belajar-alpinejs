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
  </ol>
</details>

# Tentang Repo

Repo ini saya buat sebagai riwayat sekaligus rangkuman belajar materi AlpineJS.  
Materi ini saya dapat dari berbagai sumber, tapi berpatok kepada [Video YT @TheCodeholic](https://youtu.be/5ILDMMLgX0E) karena materinya lengkap, langsung studi kasus membuat component, dan menambahkan plugin.  
Versi AlpineJS yang saya gunakan adalah versi 3.12.1

# Introduction

> Your new, lightweight, JavaScript framework

- Kalo kata dosen kita semua (Pak Sandhika Galih), AlpineJS adalah TailwindCSS versi Javascript. Jadi kita menuliskan kode javascript langsung di file html, lebih tepatnya sebagai property tag html.
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
- jika x-text berisi format text selain string seperti tag html, maka data yang ditampilkan akan berupa hardcode (diconvert ke string dan tidak mengikuti aturan html)

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

# Judul

<p align="right"><a href="#top">Go 🔝</a></p>
