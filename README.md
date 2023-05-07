# Build a Responsive Portfolio Website Advanced Animations

## Installation

First, let’s create a new project. Then we’ll start with setting up inside.

```
npx create-react-app profile-portfolio-react
cd profile-portfolio-react
```

Next, install more [bootstrap-react](https://www.npmjs.com/package/react-bootstrap) and [bootstrap](https://www.npmjs.com/package/bootstrap) library

```
npm i react-bootstrap bootstrap
npm i react-bootstrap-icons
```

## Setup Prettier and ESLint

1. Cài đặt **prettier** là formatter mặc định cho VS Code và format on save
2. Tạo file **.editorconfig**
3. Tạo file **.prettierrc** để config prettier, việc này bảo đảm đem project này cho các máy khác nhau vẫn giữ được config
4. Cài đặt devDependencies hỗ trợ **prettier** và **eslint**

```bash
npm i prettier eslint-plugin-prettier eslint-config-prettier -D
```

5. Tạo file **.eslintrc**

```json
{
  "extends": ["react-app", "prettier"],
  "plugins": ["react", "prettier"],
  "rules": {
    "prettier/prettier": [
      "warn", 
      {
        "arrowParens": "always",
        "bracketSameLine": false,
        "bracketSpacing": true,
        "embeddedLanguageFormatting": "auto",
        "htmlWhitespaceSensitivity": "css",
        "insertPragma": false,
        "jsxSingleQuote": false,
        "printWidth": 120,
        "proseWrap": "preserve",
        "quoteProps": "as-needed",
        "requirePragma": false,
        "semi": true,
        "singleQuote": true,
        "tabWidth": 2,
        "trailingComma": "all",
        "useTabs": false,
        "vueIndentScriptAndStyle": false
      }
    ]
  }
}
```

6. Config scripts của **package.json**

```json
{
    "lint": "eslint --ext js,jsx src/",
    "lint:fix": "eslint --fix --ext js,jsx src/",
    "prettier": "prettier --check \"src/**/(**.jsx|*.js|*.scss|*.css)\"",
    "prettier:fix": "prettier --write \"src/**/(**.jsx|*.js|*.scss|*.css)\""
}
```

## Navigation

Code preview:

```js
import Container from 'react-bootstrap/Container'
import Nav from 'react-bootstrap/Nav'
import Navbar from 'react-bootstrap/Navbar'

import { useState, useEffect } from 'react'
```

```js
const [activeLink, setActiveLink] = useState('home')
  const [scrolled, setScrolled] = useState(false)

  useEffect(() => {
    const onScroll = () => {
      if (window.scrollY > 50) {
        setScrolled(true)
      } else {
        setScrolled(false)
      }
    }

    window.addEventListener('scroll', onScroll)

    return () => window.removeEventListener('scroll', onScroll)
  }, [])

  const onUpdateActiveLink = value => {
    setActiveLink(value)
  }

                                          ...
```

## Banner

Code preview:

```js
import { useState, useEffect } from 'react'
import { Col, Container, Row } from 'react-bootstrap'
import { ArrowRightCircle } from 'react-bootstrap-icons'
import headerImg from '../assets/img/header-img.svg'
```

```js
export const Banner = () => {
  const [loopNum, setLoopNum] = useState(0)
  const [isDeleting, setIsDeleting] = useState(false)
  const toRotate = ['Web Developer', 'Web Designer', 'UI/UX Designer']
  const [text, setText] = useState('')
  const [delta, setDelta] = useState(300 - Math.random() * 100)
  const period = 2000

  useEffect(() => {
    let ticker = setInterval(() => {
      tick()
    }, delta)

    return () => {
      clearInterval(ticker)
    }
  }, [text])

  const tick = () => {
    let i = loopNum % toRotate.length
    let fullText = toRotate[i]
    let updatedText = isDeleting ? fullText.substring(0, text.length - 1) : fullText.substring(0, text.length + 1)

    setText(updatedText)

    if (isDeleting) {
      setDelta(prevDelta => prevDelta / 2)
    }

    if (!isDeleting && updatedText === fullText) {
      setIsDeleting(true)
      setDelta(period)
    } else if (isDeleting && updatedText === '') {
      setIsDeleting(false)
      setLoopNum(loopNum + 1)
      setDelta(500)
    }
  }
```

