----------
# 1 Headings
使用1至6个#标识标题，标题与#号间留一个空格
```
=======
# 一级标题
## 二级标题
### 三级标题

```

# 一级标题
## 二级标题
### 三级标题

----------

# 2 Styling text
使用加粗、倾斜、删除线强调文本

|style|syntax|example|output|
|-----|------|-------|------|
|粗体| \*\*text\*\*|`** This is bold text**`|**This is bold text**|
|倾斜|\_text\_|`_This is italic text_`|_This is italic text_|
|粗体加倾斜|\*\*\_ text \_\*\*|` **_This is bold and italic text_** `|**_This is bold and italic text_**|
|删除线|\~\~text\~\~|`~~This was mistaken text~~`|~~This was mistaken text~~|

----------

# 3 引用文本
使用\>引用文本

```
莎士比亚说
> 书籍是全世界的营养品
```

莎士比亚说
> 书籍是全世界的营养品

----------
# 4 应用代码
\`\`\` 符号可以引用改代码

Hello World:
```
int main()
{
	printf("hello world\n");
}
```
----------
# 5 链接
## 绝对地址
使用\[\]创建链接文本，\(\)包含链接地址

``` 
点击[这里](https://github.com)跳转到github 
```
点击[这里](www.github.com)跳转到github

## 相对链接
使用相对地址链接到本地的文件

```
[markdown logo](res/images/markdown/markdown.jpg)
```
[markdown logo](res/images/markdown/markdown.jpg)

------

# 6 列表
## 无序列表
使用\*或者\-可以创建无序列表

```
- 秦始皇
- 汉武帝
- 唐太宗
- 宋太祖
```
- 秦始皇
- 汉武帝
- 唐太宗
- 宋太祖

## 有序列表
使用数字创建有序列表


```
1. 秦始皇
2. 汉武帝
3. 唐太宗
4. 宋太祖
```
1. 秦始皇
2. 汉武帝
3. 唐太宗
4. 宋太祖

## 嵌套列表

可以使用\*或者\-通过缩进创建列表

```
1. 第一条 balabalabala
   - 第一款 balabalabala
     - 第一项 balabalabalaba

```
1. 第一条 balabalabala
   - 第一款 balabalabala
     - 第一项 balabalabalaba

----------

# 7 任务列表
使用\-\[&nbsp;\]标识未完成，使用\-\[x\]标识完成
```
- [x] 修改代码
- [ ] 添加代码
- [ ] 推送代码

```
- [x] 修改代码
- [ ] 添加代码
- [ ] 推送代码


# 8 图片

```
![markdown logo](res/images/markdown/markdown.jpg)
```

![markdown logo](res/images/markdown/markdown.jpg)