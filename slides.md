---
theme: seriph
class: text-center
highlighter: shikiji
background: './images/1.jpeg'
fonts:
  # 基础字体
  sans: 'Robot'
  # 与 windicss 的 `font-serif` css 类一同使用
  serif: 'Robot Slab'
  # 用于代码块、内联代码等
  mono: 'Fira Code'
---

# 如何编写防御式CSS

---

# 什么是防御式CSS

<div class="flex items-center px-10 text-gray-500 text-2xl h-3/4">
    <div>
        <carbon-thumbs-up-filled  class="text-purple-400 mr-2"/>一句话总结：这是一套CSS实践，设计者和开发者可以用它来编写面向未来的CSS，从而减少用户界面中的错误。
    </div>
</div>

---

# 什么是防御式CSS

<div class="text-gray-500 text-xl">
    对于开发者而言，可以把它看作是一种高级的CSS重置。
</div>

```css
/* [1] Break words when there is enough space */
h1,
h2,
h3,
h4,
h5,
h6,
p,
a {
  overflow-wrap: break-word; /* [1] */
}

/*
[1] Set a maximum width for an image
[2] Let the image cover its bounding box to avoid distortion.
*/
img {
  max-width: 100%; /* [1] */
  object-fit: cover; /* [2] */
}
```

---
layout: two-cols
---

# 总览

<div class="flex flex-col gap-3">
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />弹性盒子换行
    </div>
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />图像失真
    </div>
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />超长内容
    </div>
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />组件间距
    </div>
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />Auto-fit Vs Auto-fill
    </div>
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />背景重复
    </div>
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />CSS变量回退值
    </div>
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />固定尺寸
    </div>
</div>

::right::

<div class="flex flex-col gap-3 mt-14">
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />Flex中的最小内容尺寸
    </div>
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />图像最大宽度
    </div>
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />z-index失效
    </div>
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />滚动穿透
    </div>
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />滚动条宽度
    </div>
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />图像上的文本
    </div>
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />图像内边框
    </div>
</div>

---

# 弹性盒子换行

<div class="flex flex-col gap-3 text-gray-500 text-xl">
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />问题：当弹性盒子的内容超出容器的宽度时，会发生什么？
    </div>
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />回答：默认情况下，弹性盒子会缩小以适应容器的宽度（因为flex-shrink默认值为1）。但是默认情况下不会换行。
    </div>
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />方案：如果你想要换行，你需要使用flex-wrap属性。
    </div>
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />建议：在你的CSS中，为所有的弹性盒子容器添加flex-wrap: wrap。
    </div>
</div>

Tips：
<div class="flex flex-col gap-3">
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />flex-shrink: 0 可以防止弹性盒子缩小。
    </div>
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />flex-grow: 0 可以防止弹性盒子扩大。
    </div>
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />flex: 1 的全称是flex: 1 1 0%。
    </div>
</div>


```css{3}
.container {
  display: flex;
  flex-wrap: wrap;
}
```

---

# 图像失真

<div class="flex flex-col gap-3 text-gray-500 text-xl">
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />问题：当图片的宽高不符合容器的宽高比时，会发生什么？
    </div>
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />回答：当图片的宽高比与容器的宽高比不同时，图片会被拉伸或压缩。
    </div>
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />方案：使用object-fit: cover来避免图片失真。
    </div>
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />建议：在你的CSS中，为所有的图片添加object-fit: cover。
    </div>
</div>

Tips：
<div class="flex flex-col gap-3">
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />object-fit: cover 会保持图片的长宽比，同时填充整个容器。
    </div>
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />object-fit: contain 会保持图片的长宽比，同时保证图片完整地显示在容器中。
    </div>
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />background-size 相关属性也可以实现类似的效果。
    </div>
</div>

```css{2}
img {
  object-fit: cover;
}
```

---

# 超长内容

<div class="flex flex-col gap-3 text-gray-500 text-xl">
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />问题：当文本内容超出容器的宽度时，会发生什么？
    </div>
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />回答：文本内容会溢出容器，或者换行。
    </div>
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />方案：对文本进行截断。
    </div>
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />建议：使用TailwindCSS的truncate类，或者全局声明truncate类。
    </div>
</div>

Tips：
<div class="flex flex-col gap-3">
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />合理使用min-*和max-*属性，可以避免内容溢出容器。
    </div>
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />width: fit-content 可以让容器的宽度自适应内容的宽度。
    </div>
</div>

```css
.truncate {
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
}
```

---

# 组件间距

<div class="flex flex-col gap-3 text-gray-500 text-xl">
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />问题：当组件之间的间距不一致或者缺失时，会发生什么？
    </div>
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />回答：当组件之间的间距不一致时，会让页面整体不协调。
    </div>
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />方案：使用 margin 和 padding 来控制组件之间的间距。
    </div>
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />建议：确保组件之间具有间距。
    </div>
</div>

Tips：
<div class="flex flex-col gap-3">
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />注意外边距重叠的问题。可以通过BFC的方式避免此类问题。
    </div>
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />使用 margin 来控制元素之间的间距，使用 padding 来控制元素内部内容与边框之间的间距。
    </div>
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />使用TailwindCSS的间距类（比如m-4、p-4）。
    </div>
</div>

---
layout: two-cols
---

# Auto-fit Vs Auto-fill

<div class="flex flex-col gap-3 text-gray-500 text-xl mr-5">
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />问题：当在grid布局中展示不确定数量的元素时，应该使用 auto-fit 还是 auto-fill ？
    </div>
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />回答：auto-fit 关键字将会扩展grid子元素，来填充可用空间。而 auto-fill 将保留可用空间，不改变grid子元素的宽度。
    </div>
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />方案：如果你想要元素的大小保持一致，使用 auto-fill。如果你想要元素的大小随着空间的变化而变化，使用 auto-fit。
    </div>
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />建议：大部分情况下，我们不希望元素的大小随着空间的变化而变化，所以我们应该使用 auto-fill。
    </div>
</div>

::right::

# 图例

<img src="/images/auto-fill-fit.png" class="h-52">

```css
.wrapper {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
    grid-gap: 1rem;
}
```

---

# 背景重复

<div class="flex flex-col gap-3 text-gray-500 text-xl">
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />问题：默认情况下，背景图片会重复显示，如何避免背景图片重复显示？
    </div>
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />回答：使用 background-repeat: no-repeat，可以避免背景图片重复显示。
    </div>
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />方案：显式使用 background-repeat: no-repeat。
    </div>
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />建议：除非你想要背景图片重复显示，否则应该总是显式使用 background-repeat: no-repeat。
    </div>
</div>

Tips：
<div class="flex flex-col gap-3">
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />注意 background 的缩写格式。
    </div>
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />一个元素可以有多个背景图，使用逗号分隔。越靠左的背景图越先展示。
    </div>
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />因此当展示异步加载的背景图时，应该把占位图放在最后。
    </div>
</div>

```css{3}
.background {
    background-image: url('..');
    background-repeat: no-repeat;
}
```

---

# CSS变量回退值

<div class="flex flex-col gap-3 text-gray-500 text-xl">
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />问题：当使用未声明的CSS变量时，会发生什么？
    </div>
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />回答：该属性将被解析为无效值，可能导致样式不生效。
    </div>
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />方案：在使用CSS变量时，总是提供一个回退值。
    </div>
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />建议：同上。
    </div>
</div>

Tips：
<div class="flex flex-col gap-3">
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />font-family、image()同样支持使用回退值。
    </div>
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />CSS变量可以直接参与计算，比如：max-width: calc(100% - var(--actions-width, 70px))。
    </div>
</div>

```css{2}
.element {
    color: var(--color, #000);
}
```

---

# 固定尺寸

<div class="flex flex-col gap-3 text-gray-500 text-xl">
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />问题：对按钮组件使用固定宽度，会发生什么？
    </div>
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />回答：当按钮组件的文本内容超出固定宽度时，会发生溢出。
    </div>
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />方案：合理使用 min-width 和 max-width 来控制组件的宽度。
    </div>
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />建议：在响应式设计中，应该尽量避免使用固定尺寸。
    </div>
</div>

Tips：
<div class="flex flex-col gap-3">
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />在国际化的场景中，可能需要区分物理属性和逻辑属性。
    </div>
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />在逻辑属性中，width 对应的就是 inline-size，height 对应的就是 block-size。
    </div>
</div>

```css{2}
.button {
    min-width: 100px;
}
```

---
layout: two-cols
---

# Flex中的最小内容尺寸

<div class="flex flex-col gap-3 text-gray-500 text-xl mr-4">
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />问题：如果flex子元素有一个文本元素或者图像，其比子元素本身要大，会发生什么？
    </div>
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />回答：此时，浏览器并不会缩放它们，哪怕使用 overflow-wrap: break-word 换行也不行。
    </div>
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />方案：使用 min-width: 0 来解决这个问题。这是因为 min-width 的默认值是auto，会产生溢出。
    </div>
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />建议：在你的CSS中，为flex子元素添加 min-width: 0。
    </div>
</div>

```css{3}
.card__title {
    overflow-wrap: break-word;
    min-width: 0;
}
```

::right::

# 图例

<img src="/images/flex.png" class="h-52">

Tips：
<div class="flex flex-col gap-3">
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />如果 Flex 项目的 flex-basis 和 width 取初始值 auto 时，Flex 项目的初始化尺寸是 fit-content。
    </div>
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />Flexbox 布局中要实现均分列（等分列）布局效果时，请在 Flex 项目上显式设置 min-width 的值为 0 ，避免因内容不等长，造成列不均等 。
    </div>
</div>

---

# 图像最大宽度

<div class="flex flex-col gap-3 text-gray-500 text-xl mr-4">
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />问题：当图像的宽度非常大时，会发生什么？
    </div>
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />回答：此时，图像会溢出容器，导致页面布局混乱。
    </div>
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />方案：使用 max-width: 100% 来解决这个问题。
    </div>
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />建议：在全局CSS中，为所有的img添加 max-width: 100%。
    </div>
</div>

Tips：
<div class="flex flex-col gap-3">
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />元素的 width 大于或等于 max-width 时，取 max-width ，即 max-width 能覆盖 width ；
    </div>
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />元素的 width 小于或等于 min-width 时，取 min-width ，即 min-width 能覆盖 width ；
    </div>
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />当 min-width 大于 max-width 时，取 min-width ，即 min-width 优先级将高于 max-width 。
    </div>
</div>

```css
img {
    max-width: 100%;
    object-fit: cover;
}
```
---

# z-index失效

<div class="flex flex-col gap-3 text-gray-500 text-xl mr-4">
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />问题：明明指定了一个更大的 z-index 值，怎么层级就是上不去呢？
    </div>
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />回答：这是因为 z-index 只作用于当前的层叠上下文中。
    </div>
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />方案：需要指定元素的 position 属性值是一个非 static值，比如 relative、absolute。
    </div>
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />建议：层叠等级需要在相同的层叠上下文中比较才有意义，不同层叠上下文中比较层叠等级是没有意义的。
    </div>
</div>

Tips：
<div class="flex flex-col gap-3">
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />检查元素是否创建层叠上下文和按正确的顺序设置了它们的 z-index ；
    </div>
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />确保没有父元素限制其子元素的 z-index 级别。
    </div>
</div>

```css
.parent {
    position: relative;
    z-index: 1;
}
```

---

# 滚动穿透

<div class="flex flex-col gap-3 text-gray-500 text-xl mr-4">
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />问题：打开一个模态框并开始滚动，当你滚动到底并继续滚动时，模态框下面的内容将开始滚动（如果有滚动条的话），这是为什么？
    </div>
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />回答：这种现象称为滚动穿透，需要设置CSS或者JS来避免。
    </div>
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />方案：在滚动容器上显式设置 overscroll-behavior: contain。
    </div>
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />建议：在模态框组件的滚动容器添加 overscroll-behavior: contain。
    </div>
</div>

Tips：
<div class="flex flex-col gap-3">
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />在Vant的Overlay组件中，提供 lock-scroll 来锁定背景滚动。副作用是蒙层里的内容也将无法滚动。
    </div>
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />核心原理是通过监听 touchmove 事件并 preventDefault 来阻止滚动。
    </div>
</div>

```css
.scroll--container {
    overflow: auto; /* 可以是  overflow-x 或 overflow-y */
    scrollbar-gutter: stable; /* 如果有需要的就设置 */
    overscroll-behavior: contain; /* 如果要阻止下拉刷新的话，请使用 none */
    scroll-behavior: smooth; /* 提供丝滑般滚动效果 */
}

```

---

# 滚动条宽度

<div class="flex flex-col gap-3 text-gray-500 text-xl mr-4">
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />问题：当内容变得更长时，添加滚动条会导致布局改变，这是为什么？
    </div>
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />回答：这是因为滚动条的宽度会占用容器的宽度。此时会导致容器的宽度变小。
    </div>
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />方案：使用 CSS 的 scrollbar-gutter 属性为滚动条提前预留空间，避免页面布局的变化。
    </div>
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />建议：使用scrollbar-gutter: stable来避免因为滚动条的出现而导致布局变化。
    </div>
</div>

Tips：
<div class="flex flex-col gap-3">
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />滚动条的类型，它主分为经典型滚动条（Windows）和覆盖式滚动条（Mac）。
    </div>
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />在 element-plus 的Dialog组件中，提供了 lock-scroll 属性来将 body 滚动锁定。
    </div>
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />核心原理是动态添加 hiddenCls 类来隐藏滚动条，同时要减去滚动条的宽度。
    </div>
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />也可以直接使用 winbox 或者 element-plus 中提供的 scrollbar 组件。
    </div>
</div>

```css
.element {
    scrollbar-gutter: stable;
}
```

---

# 图像上的文本

<div class="flex flex-col gap-3 text-gray-500 text-xl mr-4">
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />问题：当在图像上使用文本时，考虑图像无法加载的情况是很重要的，此时文本会是什么样子？
    </div>
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />回答：文字可能会与默认白色背景融为一体，导致无法阅读。
    </div>
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />方案：给图像元素上添加背景颜色，避免文字与背景融为一体。
    </div>
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />建议：要考虑图像无法加载的情况，给图像元素添加背景颜色。
    </div>
</div>

还可以考虑其他方案：
<div class="flex flex-col gap-3">
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />文本和图片之间添加一个渐变层；
    </div>
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />文本和图片之间添加一个带透明度的颜色层；
    </div>
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />给文本添加阴影；
    </div>
    <div>
        <carbon-next-filled class="text-lg text-purple-400 mr-2" />让文本变得高亮。
    </div>
</div>

```css
.card__img {
    background-color: grey;
}
```

---
layout: two-cols
---

# 图像内边框

<div class="flex flex-col gap-3 text-gray-500 text-xl mr-4">
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />问题：当处理用户头像时，用一种清晰的方式展示头像是具有挑战性的。是因为有些图像太亮，因此它可能与下面的背景融合在一起，尤其是白色。
    </div>
    <div>
        <carbon-user-online class="text-lg text-purple-400 mr-2" />方案：为图像添加内边框。我们需要将图像包裹在另一个元素中，并对其施加内阴影。
    </div>
</div>

<img src="/images/border.png" class="h-52">

::right::

```html
<div class="card__avatar">
  <img src="assets/shadeed.jpg" alt="" />
  <div class="border"></div>
</div>
```

```css
.card__avatar {
    position: relative;
}

.card__avatar img {
    width: 56px;
    height: 56px;
    border-radius: 50%;
}

.border {
    position: absolute;
    width: 56px;
    height: 56px;
    border: 2px solid #000;
    border-radius: 50%;
    opacity: 0.1;
}
```

---

# 总结

<div class="flex items-center px-10 text-gray-500 text-2xl h-1/2">
    <div>
        <carbon-thumbs-up-filled  class="text-purple-400 mr-2"/>通过采用防御式CSS的方法，我们可以编写更健壮、可维护的CSS代码，减少样式冲突和问题，并提高开发效率和用户体验。
    </div>
</div>

参考链接：

<carbon-link class="text-lg text-purple-400 mr-2" />[https://defensivecss.dev/](https://defensivecss.dev/)

<div class="my-3"></div>

<carbon-link class="text-lg text-purple-400 mr-2" />[防御式CSS精讲](https://juejin.cn/book/7199571709102391328)

---

<div class="flex items-center justify-center px-10 text-gray-700 text-4xl h-3/4">
    <div>
        Thanks!
    </div>
</div>