---
title: js通过url下载文件
categories:
  - js
tags:
  - fetch
mp3: /music/挪威森林-伍佰.mp3
cover: /img/55b91170d5bb2a0a2e323a9709a4a7a9.jpg
date: 2022-11-26 14:34:26
---
```javascript
fetch(src).then(res => res.blob().then(blob => {
  let a = document.createElement('a');
  let url = window.URL.createObjectURL(blob);
  a.href = url;
  a.download = name;
  a.click();
  window.URL.revokeObjectURL(url);
}))
```