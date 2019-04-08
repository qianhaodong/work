# CSS

### 介绍一下标准的CSS的盒子模型？低版本IE的盒子模型有什么不同的？

有两种：IE盒子模型、w3c盒子模型

- 盒模型：内容（content）、填充（padding）、边框（border）、边界（margin）
- 区别：IE的 content 部分把 border 和 padding 计算了进去；

---



### display有哪些值？说明他们的作用？

1. block		块类型。默认宽度为父元素宽度，可设置宽高，换行显示；
2. none                元素不现实，并从文档流中移除；
3. inline                行内元素类型。默认宽度为内容宽度，不可设置宽高，同行显示；
4. inline-block     行内块元素类型。默认宽度为内容宽度，可以设置宽高，同行显示；
5. list-item           象块类型元素一样显示，并添加样式列表标记；
6. table                此元素会作为块级表格来显示；
7. inherit              规定应该从父元素继承 display 属性的值；

---



### 对BFC规范的理解？

定义：BFC（block formatting context）直译为“块级格式化上下文”。它是一个独立的渲染区域，并且这个区域与外部毫不相干；

**触发条件：**

1. float 的值不为 none；
2. overflow 的值不为 visible；
3. display 的值为 inline-block、table-cell、table-caption；
4. position 的值为 absolute 或 fixed；

**BFC有哪些作用**

1. 可以阻止元素被浮动元素覆盖；
2. 可以包含浮动元素（清除内部浮动）；
3. 不同的BFC元素可以阻止 margin 重叠；

---



### 请解释一下为什么需要清除浮动？清除浮动的方式？

清除浮动是为了清除使用浮动元素产生的影响。浮动的元素，高度会塌陷，而高度的塌陷使其他的页面元素布局不能正常显示；

1. 父级元素定义高度（height）

2. 父级元素也一起浮动

3. 使用伪元素清除浮动（添加一个class）

   ```html
   .clearfix::after {
   	content: '';
   	clear: both;
   	height: 0;
   	display: block;
   	visibility: hidden;
   }
   .clearfix {
   	*zoom: 1;
   }
   ```

**解析原理：**

- display: block 使生成的元素以块级元素显示，占满剩余空间；
- height: 0 避免生成内容破坏原有的布局的高度；
- visibility：hidden 使生成的内容不可见，并允许可能被生成内容盖住的内容可以进行点击和交互;
- zoom：1 触发 IE 的 hasLayout

---



### CSS优化、提高性能的方法有哪些？

1. **加载性能：**

   - css 压缩：将写好的 css 进行打包压缩，可以减少很多的体积；
   - 减少使用 @import，而建议使用 link，因为后者在页面加载时一起加载，前者是等待页面加载完成之后再进行加载；

2. **选择器性能：**

   css 选择器是从右到左进行匹配的。当使用后代选择器的时候，浏览器会遍历所有子元素来确定是否是指定的元素等等；

   - 避免使用通配符选择器
   - 尽量少的去对标签进行选择，而是使用 class
   - 尽量少的去使用后代选择器，降低选择器的权重值（后代选择器的开销是最高的，尽量将选择器的深度降到最低，最高不要超过三层）

3. **渲染性能：**

   - 慎重使用高性能属性：浮动、定位
   - 使用 css 雪碧图，减少页面的请求次数

4. **可维护性、健壮性：**

   - 将具有相同属性的样式抽离出来，整合并通过 class 在页面中进行使用，提高 css 的可维护性；
   - 样式与内容分离：将 css 代码定义到外部 css 中；

---



### 移动端适配方案？

1. Media Queries（媒体查询）

   主要是通过查询设备的宽度来执行不同的 css 代码，最终达到界面的配置；

2. flex 弹性布局

3. rem 布局（通过 JS 控制 rem 的基准值）

   ```javascript
   (function(win,doc) {
       if (!win.addEventListener) return;
       var html = document.documentElement;
       function setFont() {
           var w = html.clientWidth,
               h = html.clientHeight;
           html.style.fontSize = (w < h ? w/750*100 : w/1334*100) + 'px';
       }
       setFont();
       doc.addEventListener('DOMContentLoaded', setFont, false);
       win.addEventListener('resize', setFont, false);
       win.addEventListener('load', setFont, false);
   })(window,docment);
   ```



