
> 😀 都是跑通过的bash命令。


## 目录下文件类型统计

```bash
find . -type f | awk -F. '{if (NF==1) print "no_extension"; else print $NF}' | sort | uniq -c | sort -nr | awk '{print $2, $1}'
```

yysy，awk真的很强大，至今还是没学会咋用。。。

## 类型文件数量统计

```bash
find . -type f \( -iname "*.png" -o -iname "*.bmp" -o -iname "*.tif" -o -iname "*.tiff" -o -iname "*.jpg" -o -iname "*.jpeg" -o -iname "*.gif" -o -iname "*.webp" \) | wc -l
```

## 条件拷贝，并保持目录结构

```bash
find <source_path> -type f -name '*-Color-*' -exec cp --parents -t <target_path> {} +
```

## tree

| **功能** | **arg** | **举例** |
| --- | --- | --- |
| 指定深度 | -L | `tree . -L 3 \| wc -l` |
|  |  |  |
|  |  |  |

## find查找项目

```bash
find / -iname "*{被查找}*" 2>/dev/null
```

-iname 进行大小写不敏感的搜索。

## git bash

复制目录时，对比复制前后的总大小：

```bash
du -s --apparent-size <folder_path>
```

- --apparent-size: 显示实际大小
- -s: 合计
