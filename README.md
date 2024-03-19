### tips

=> 教程进度4.1

1、pages 目录下的文件会自动创建 `router`， 以供访问
2、css style 可以使用 `frontmatter`  中的变量

```
---
const textColor = 'red'
const textSize = 12
---

<style define:vars={{textColor, textSize}}>
    .text {
        font-size: var(--textSize);
        color: var(--textColor)
    }
</style>
```

3、组件使用

- 引用方式与 vue 、react 方式无区别
- 组件的传值也是在 Component 上设置属性参数传递给该组件，组件内读取使用 `Astro.props` 即可
- 因为服务端渲染的缘故 `frontmatter` 中不能访问 document 对象，通常是在 html 部分中的 `<script>` 标签内完成


