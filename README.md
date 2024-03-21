### tips

=> 基础教程进度 Finish

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

- 引用方式与正常引入模块一样，使用 `import` 关键字引入
- 因为服务端渲染的缘故 `frontmatter` 中不能访问 `document` 对象，通常是在 `html` 部分中的 `<script>` 标签内完成
- 组件的传值也是在 `Component` 上设置属性参数传递给该组件，组件内读取使用 `Astro.props` 即可
- 插槽： `<slot />` 允许你将写在开放和闭合 `<Component></Component>` 标签之间的子内容注入到任何 Component.astro 文件中。
- 基于组件的设计，布局不仅可以复用，同时布局组件之间可以进行嵌套，实现复杂的页面布局

4、markdown 的解析

- 文件中的 `YAML frontmatter` 中的属性会被解析为 `props` 传递给在文件头部指定的 `layout` 属性指向的模板组件，
  并在组件中使用 `Astro.props` 获取

5、`Astro` 的 Api

- `const allPosts = await Astro.glob('../pages/posts/*.md')` 获取所有的 `markdown` 文件
- **动态路由匹配**
    - 与 vue 在 `router` 中的配置项目 `:id` 不同，`Astro` 中是以文件目录生成路由信息的；以 `[]` 包裹的文件名会被视为动态路由
    - `getStaticPaths` 方法是动态组件的必须方法，用于生成动态路由的匹配的信息，只有在 `getStaticPaths` 中返回的 `paths`
      中的路径才会被匹配到
    - `getStaticPaths` 的返回值是一个对象数组，数组的每一项是一个对象, 而这个对象就是当路由被匹配到时，`Astro` 会将这个对象传递给组件

        - 对象中的 `params` 属性直接匹配到浏览器地址栏中的 `[]` 中的值，在 `frontmatter`
          中（除了函数内部）可以通过 `Astro.params` 获取
        - 对象中的 `props` 属性则可以通过 `Astro.props` 获取

6、 rss 订阅

> 按照流程即可：https://docs.astro.build/zh-cn/tutorial/5-astro-api/4/
