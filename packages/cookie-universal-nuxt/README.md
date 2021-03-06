# cookie-universal-nuxt
[![npm (scoped with tag)](https://img.shields.io/npm/v/cookie-universal-nuxt/latest.svg?style=flat-square)](https://npmjs.com/package/cookie-universal-nuxt)
[![npm](https://img.shields.io/npm/dt/cookie-universal-nuxt.svg?style=flat-square)](https://npmjs.com/package/cookie-universal-nuxt)
[![js-standard-style](https://img.shields.io/badge/code_style-standard-brightgreen.svg?style=flat-square)](http://standardjs.com)

> Universal cookie plugin for Nuxt, perfect for SSR

You can use `cookie-universal-nuxt` to set, get and remove cookies in both client and server side nuxt apps.
`cookie-universal-nuxt` parse cookies with the popular [cookie node module](https://github.com/jshttp/cookie).

## Install
- yarn: `yarn add cookie-universal-nuxt`
- npm: `npm i --save cookie-universal-nuxt`

Add `cookie-universal-nuxt` to `nuxt.config.js`:

```js
{
  modules: [
    // Simple usage
    'cookie-universal-nuxt',

    // With options
    ['cookie-universal-nuxt', { alias: 'cookiz' }],
 ]
}
```

## Api

<details><summary><code>set(name, value, opts)</code></summary><p>

- `name` (string): Cookie name to set.
- `value` (string|object): Cookie value.
- `opts` (object): Same as the [cookie node module](https://github.com/jshttp/cookie). 
  - `path` (string): Specifies the value for the Path Set-Cookie attribute. By default, the path is considered the "default path".
  - `expires` (date): Specifies the Date object to be the value for the Expires Set-Cookie attribute. 
  - `maxAge` (number): Specifies the number (in milliseconds) to be the value for the Max-Age Set-Cookie attribute.
  - `httpOnly` (boolean): Specifies the boolean value for the [HttpOnly Set-Cookie attribute][rfc-6265-5.2.6].
  - `domain` (string): specifies the value for the Domain Set-Cookie attribute. 
  - `encode` (function): Specifies a function that will be used to encode a cookie's value.  
  - `sameSite` (boolean|string): Specifies the value for the Path Set-Cookie attribute. By default, the path is considered the "default path". 
  - `secure` (boolean): Specifies the boolean value for the Secure Set-Cookie attribute. 

```js
const cookieValObject = { param1: 'value1', param2: 'value2' }

// server
app.$cookies.set('cookie-name', 'cookie-value', { 
  path: '/',
  maxAge: 60 * 60 * 24 * 7
})
app.$cookies.set('cookie-name', cookieValObject, { 
  path: '/',
  maxAge: 60 * 60 * 24 * 7
})

// client
this.$cookies.set('cookie-name', 'cookie-value', { 
  path: '/',
  maxAge: 60 * 60 * 24 * 7
})
this.$cookies.set('cookie-name', cookieValObject, { 
  path: '/',
  maxAge: 60 * 60 * 24 * 7
})
```
</p></details>

---

<details><summary><code>setAll(cookieArray)</code></summary><p>

- cookieArray (array)
  - `name` (string): Cookie name to set.
  - `value` (string|object): Cookie value.
  - `opts` (object): Same as the [cookie node module](https://github.com/jshttp/cookie) 
    - `path` (string): Specifies the value for the Path Set-Cookie attribute. By default, the path is considered the "default path".
    - `expires` (date): Specifies the Date object to be the value for the Expires Set-Cookie attribute. 
    - `maxAge` (number): Specifies the number (in milliseconds) to be the value for the Max-Age Set-Cookie attribute.
    - `httpOnly` (boolean): Specifies the boolean value for the [HttpOnly Set-Cookie attribute][rfc-6265-5.2.6].
    - `domain` (string): specifies the value for the Domain Set-Cookie attribute. 
    - `encode` (function): Specifies a function that will be used to encode a cookie's value.  
    - `sameSite` (boolean|string): Specifies the value for the Path Set-Cookie attribute. By default, the path is considered the "default path". 
    - `secure` (boolean): Specifies the boolean value for the Secure Set-Cookie attribute. 

```js
const options = {
  path: '/',
  maxAge: 60 * 60 * 24 * 7
}
const cookieList = [
  { name: 'cookie-name1', value: 'value1', opts: options },
  { name: 'cookie-name2', value: 'value2', opts: options },
  { name: 'cookie-name3', value: 'value3', opts: options },
  { name: 'cookie-name4', value: 'value4', opts: options }
]

// server
app.$cookies.setAll(cookieList)

// client
this.$cookies.setAll(cookieList)
```
</p></details>

---

<details><summary><code>get(name, fromRes)</code></summary><p>

- `name` (string): Cookie name to get.
- `fromRes` (boolean): Get cookies from res instead of req.
 
```js
// server
const cookieRes = app.$cookies.get('cookie-name') 
const cookieRes = app.$cookies.get('cookie-name', true) // get from res instead of req 
// returns the cookie value or undefined

// client
const cookieRes = this.$cookies.get('cookie-name') 
// returns the cookie value or undefined
```
</p></details>

---

<details><summary><code>getAll(fromRes)</code></summary><p>

- `fromRes` (boolean): Get cookies from res instead of req.

```js
// server
const cookiesRes = app.$cookies.getAll() 
const cookiesRes = app.$cookies.getAll(true) // get from res instead of req 
// returns all cookies or []
[
  {
    "name": "cookie-1",
    "value": "value1"
  },
  {
    "name": "cookie-2",
    "value": "value2"
  }
]

// client
const cookiesRes = this.$cookies.getAll() 
// returns all cookies or []
[
  {
    "name": "cookie-1",
    "value": "value1"
  },
  {
    "name": "cookie-2",
    "value": "value2"
  }
]
```
</p></details>

---

<details><summary><code>remove(name, opts)</code></summary><p>

- `name` (string): Cookie name to remove.
- `opts` (object): The only option available is path. Use it to remove the cookie from a specific location.
  
```js
// server
app.$cookies.remove('cookie-name') 
app.$cookies.remove('cookie-name', {
  // this will allow you to remove a cookie
  // from a different path
  path: '/my-path' 
})

// client
this.$cookies.remove('cookie-name') 
```
</p></details>

---

<details><summary><code>removeAll()</code></summary><p>

```js
// note that removeAll does not currently allow you 
// to remove cookies that have a 
// path different from '/'

// server
app.$cookies.removeAll() 

// client
this.$cookies.removeAll() 
```
</p></details>

---

<details><summary>Plugin options</summary><p>

- `alias` (string): Specifies the plugin alias to use

```js
{
  modules: [
    ['cookie-universal-nuxt', { alias: 'cookiz' }],
 ]
}


// usage
this.$cookiz.set('cookie-name', 'cookie-value')
```
</p></details>

## License

[MIT License](./LICENSE)

Copyright (c) Salvatore Tedde <microcipcip@gmail.com>
