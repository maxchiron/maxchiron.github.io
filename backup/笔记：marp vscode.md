## 创建双栏页

声明：
```html
<!-- two column style -->
<style>
.container{
  display: flex;
}
.col{
  flex: 1;
}
</style>
```

使用：
```html
<div class="container">
    <div class="col">
        Column 1 Content
    </div>
    <div class="col">
        Column 2 Content
    </div>
</div>
```

## 超小字（脚注）

```html
<br><br><br><span style="font-size: 15px;">超小字内容</span>
```

## 上标（索引|引用）

```html
<sup>1</sup>
```

## 内嵌mermaid

```html
<!-- mermaid.js -->
<script src="https://unpkg.com/mermaid@10.5.0/dist/mermaid.js"></script>
<script>mermaid.initialize({startOnLoad:true, theme:'forest'});</script>

<pre class="mermaid">
    %%{init: { 'theme': 'forest' }}%%
    graph LR
        A[输入问题] --> B(( LLM ))
        B --> C[回答]
        D[输入问题] --> E(( R M ))
        E --> F[思考过程 + 回答]
</pre>
```