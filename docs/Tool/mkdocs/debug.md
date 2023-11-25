# 一些Debug

## 关于数学符号渲染的配置

在mkdocs.yml下添加如下指令

```yml
markdown_extensions:
  - pymdownx.arithmatex:
    generic: true
```

```yml
extra_javascript:
  - https://polyfill.io/v3/polyfill.min.js?features=es6
  - https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js
```

**务必要将配置放在nav之前！**

[更多](https://facelessuser.github.io/pymdown-extensions/extensions/arithmatex/)