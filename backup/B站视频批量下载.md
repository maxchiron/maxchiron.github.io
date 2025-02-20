
> [https://www.bilibili.com/opus/927702172755296257](https://www.bilibili.com/opus/927702172755296257)

## Step 1

进入待下载页面。例如：

![Image](https://github.com/user-attachments/assets/85f93cfc-4675-47d5-805b-82f2288c38ae)

## Step 2

打开开发者工具，在控制台输入let data = []，创建一个空数组

![Image](https://github.com/user-attachments/assets/078ac491-8571-465f-a17e-84c787f4d7de)

![Image](https://github.com/user-attachments/assets/24d118f9-56de-421e-83e7-972bf982d3e2)

![Image](https://github.com/user-attachments/assets/e3fd79ea-d546-4ae3-872c-b10f5b80b8ed)

## Step 3

输入代码

`data = data.concat(Array.from(new Set(Array.from(document.querySelectorAll('a')).map(el => el.href).filter(url => url.includes('www.bilibili.com/video')))))`

![Image](https://github.com/user-attachments/assets/f16f52b8-8150-40f6-ab77-d62c6ecaba1f)

## Step 4

手动点击“下一页”后，再运行一次上述代码。
每一页都运行一次上述代码。

## Step 5

输入代码data.join(' ')，格式化收集到的链接，复制。

![Image](https://github.com/user-attachments/assets/fd33a66e-2f63-489e-a17b-a6400d1c5bd6)

## Step 6
用python + yt-dlp进行逐个下载。