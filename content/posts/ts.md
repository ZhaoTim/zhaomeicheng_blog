---
title: "TS的笔记"
date: 2023-03-29T18:48:13+08:00
---

### `keyof`

返回值为联合类型（或者的关系）

```ts
interface IArticle {
  content: string;
  authorId: number;
  category: string;
}

// 'content' | 'authorId' | 'category'
type ArticleKeys = keyof IArticle;
```

结合 typeof 操作符获取对象的 keys

```ts
const article = {
  content: 'content',
  authorId: 123,
  category: 'misc',
};

// 'content' | 'authorId' | 'category'
type ArticleKeys = keyof typeof article;
```