---
emoji: ๐ง
title: AJAX๋ ?!
date: '2022-04-05 17:30:00'
author: leedawn
tags: web
categories: web
---

์๋ฐ์คํฌ๋ฆฝํธ๋ก apiํค ์จ๊ธฐ๊ธฐ ์๋ ๐๏ธโโ๏ธ ๊ทธ๋ฌ๋ ์คํจ,,,!  
.env๋ ์นํฉ์ด ์๋ ์์ ์๋ฐ์คํฌ๋ฆฝํธ๋ก apiํค๋ฅผ ์จ๊ธฐ๊ธฐ ์ํด apikey.js์ api ๊ฐ์ฒด๋ฅผ ๋ง๋ค๊ณ , .gitignore์ apikey.js๋ฅผ ์ถ๊ฐํ์ฌ ์จ๊ธฐ๋ ๋ฐฉ๋ฒ์ ์ฌ์ฉํ๋๋ฐ..... ์ฐพ์๋ณด๋ ajax ๋ฐฉ์์ผ๋ก ๋ณด๋ด๋ ๊ฑฐ๋ผ์ ๊ฐ๋ฐ์ ๋๊ตฌ์์ ์ ๋ณด๊ฐ ์ค์ค ์๋ค๊ณ  ํ๋ค.. ์ค์ ๋ก ๋คํธ์ํฌํญ์ ์ด์ด๋ณด๋ apiํค๊ฐ ํคํ ๋ณด์ธ๋ค ๐ ๋ฌด๋ฃ api๋ผ์ ํฌ๊ฒ ์๊ด์์ง๋ง, ์ค์  ํ์์์๋ ์ด๋ค ์์ผ๋ก ์ฒ๋ฆฌํด์ผํ๋์ง ๊ถ๊ธํ๋ค..! ์ด๊ฑด ๋ค์์ ๊ธ๋ก ์ ๋ฆฌํด๋ณด๊ฒ ์ ๐ช๐ป

๊ทธ๋ ๋ค๋ฉด, ajax ๋ฐฉ์์ด๋ ๋ฌด์์ผ๊น?

### ajax

**ajax**๋ **Asynchronous JavaScript and XML**์ ์ฝ์ด๋ก, **์๋ฒ์ ๋น๋๊ธฐ์ ์ผ๋ก ๋ฐ์ดํฐ๋ฅผ ์ฃผ๊ณ ๋ฐ๋ ์๋ฐ์คํฌ๋ฆฝํธ ๊ธฐ์ **์ ์๋ฏธํ๋ค. ์น ํ์ด์ง ์ ์ฒด๋ฅผ ๋ค์ ๋ก๋ฉํ์ง ์๊ณ ๋ ์๋ฒ์ GET ์์ฒญ์ ๋ ๋ฆด ์ ์๋ js ์ฝ๋๋ผ๊ณ  ์ดํดํ๋ฉด ๋๋ค.

- ์ฅ์  : ์๋ก๊ณ ์นจ์ด ์์ผ๋๊น ์นํ์ด์ง ์ ํ์ด ๋ถ๋๋ฌ์์ง
- ํ๊ณ : Ajax๋ฅผ ์ด์ฉํ๋ฉด ์ฌ๋ฌ ์ฅ์ ์ ๊ฐ์ง์ง๋ง, Ajax๋ก๋ ๋ค์๊ณผ ๊ฐ์ ์ผ๋ค์ ์ฒ๋ฆฌํ  ์ ์๋ค.
  1. Ajax๋ ํด๋ผ์ด์ธํธ๊ฐ ์๋ฒ์ ๋ฐ์ดํฐ๋ฅผ ์์ฒญํ๋ ํด๋ผ์ด์ธํธ ํ๋ง ๋ฐฉ์์ ์ฌ์ฉํ๋ฏ๋ก, ์๋ฒ ํธ์ ๋ฐฉ์์ ์ค์๊ฐ ์๋น์ค๋ ๋ง๋ค ์ ์๋ค.
  2. Ajax๋ก๋ ๋ฐ์ด๋๋ฆฌ ๋ฐ์ดํฐ๋ฅผ ๋ณด๋ด๊ฑฐ๋ ๋ฐ์ ์ ์์.
  3. Ajax ์คํฌ๋ฆฝํธ๊ฐ ํฌํจ๋ ์๋ฒ๊ฐ ์๋ ๋ค๋ฅธ ์๋ฒ๋ก Ajax ์์ฒญ์ ๋ณด๋ผ ์๋ ์๋ค.
  4. ํด๋ผ์ด์ธํธ์ PC๋ก Ajax ์์ฒญ์ ๋ณด๋ผ ์๋ ์๋ค.

### ์๋ฐ์คํฌ๋ฆฝํธ๋ก ajax ์์ฒญ์ ๋ ๋ฆฌ๋ ๋ฐฉ๋ฒ

- fetch

```jsx
fetch('https://leedawnn.github.io/price.json')
  .then((response) => {
    if (!response.ok) {
      throw new Error('400 ์๋๋ฉด 500 ์๋ฌ๋จ');
    }
    return response.json();
  })
  .then((๊ฒฐ๊ณผ) => {
    console.log(๊ฒฐ๊ณผ);
  })
  .catch(() => {
    console.log('์๋ฌ๋จ');
  });
```

- async/await

```jsx
async function ๋ฐ์ดํฐ๊ฐ์ ธ์ค๋ํจ์() {
  const response = await fetch('https://leedawnn.github.io/price.json');
  if (!response.ok) {
    throw new Error('400 ์๋๋ฉด 500 ์๋ฌ๋จ');
  }
  const result = await response.json();
  console.log(result);
}
๋ฐ์ดํฐ๊ฐ์ ธ์ค๋ํจ์().catch(() => {
  console.log('์๋ฌ๋จ');
});
```

- axios

```jsx
axios
  .get('https://leedawnn.github.io/price.json')
  .then((result) => {
    console.log(result.data); // ์๋ฒ์์ ๋ฐ์์จ ๋ฐ์ดํฐ
  })
  .catch(() => {
    console.log('์๋ฌ๋จ');
  });
```
