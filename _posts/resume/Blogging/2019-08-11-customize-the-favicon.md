---
title: Customize the Favicon
author: Cotes Chung
date: 2019-08-11 00:34:00 +0900
categories: [Resume, Blogging]
tags: [favicon]
toc: false
comments: true
---

In [**Chirpy**](https://github.com/cotes2020/jekyll-theme-chirpy/), the image files of [Favicons](https://www.favicon-generator.org/about/) are placed in `assets/img/favicons/`. You may need to replace them with your own. So let's see how to customize these Favicons.

With a square image (PNG, JPG or GIF) in hand, open the site [*Favicon & App Icon Generator*](https://www.favicon-generator.org/) and upload your original image.

![upload-image](/assets/img/sample/upload-image.png)

Click button <kbd>Create Favicon</kbd> and wait a moment for the website to generate the icons of various sizes automatically.

![download-icons](/assets/img/sample/download-icons.png){: width="600"}

Download the generated package, unzip and delete the following two from the extracted files:

- browserconfig.xml
- manifest.json
 
Now, copy the remaining image files (`.PNG` and `.ICO`) from the extracted `.zip` file to cover the original files in the folder `assets/img/favicons/`.

The following table helps you understand the changes to the icon file:

> ✓ means keep, ✗ means delete.

| File(s)             | From Favicon & App Icon Generator | From Chirpy |
|---------------------|:---------------------------------:|:-----------:|
| `*.PNG`             | ✓                                 | ✗           |
| `*.ICO`             | ✓                                 | ✗           |
| `browserconfig.xml` | ✗                                 | ✓           |
| `manifest.json`     | ✗                                 | ✓           |


The next time you build the site, the icon will be replaced with a customized edition.

- 이미지 정렬에 참고할 만한 블로그<br>
    - [이미지 사이즈 및 정렬1](https://blog.yena.io/studynote/2017/11/23/Github-resize-image.html)
    - [이미지 사이즈 및 조절 2](https://stackoverflow.com/questions/24319505/how-can-one-display-images-side-by-side-in-a-github-readme-md)
    - [이미지뿐만 아니라 마크다운 전반적으로 설명 잘되어있는 곳](https://lynmp.com/ko/article/title/markdown-image-ob811c9dc5v0)

- 이미지 텍스트 인라인에 표시방법 ex) 이렇게 <img style="max-width: 10px; vertical-align: middle;" src="/assets/img/rightdirection.png">  표시 
```html
<img style="max-width: 원하는 픽셀값px; vertical-align: middle;" src="/이미지주소/이미지명.png"> 
``` 
- [gif 만드는 사이트 ](https://m.blog.naver.com/PostView.nhn?blogId=minzzok&logNo=221671713605&proxyReferer=https:%2F%2Fwww.google.com%2F)
    