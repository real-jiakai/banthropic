# 🔨 Banthropic — 封号是为了你好

> Claude 封号风险自测中心(非官方,比官方诚实)。

一个讽刺性质的整活单页站,灵感来自 [LinXiaoTao/FuckClaude](https://github.com/LinXiaoTao/FuckClaude)。
在浏览器本地检测时区、语言、中文字体、日期格式、emoji 渲染,并查询 IP 归属地
(数据中心 / 机房 IP 加分,「人类不住在机房里」),配合「自首环节」
(VCC、闲鱼充值、`ANTHROPIC_BASE_URL`……)算出 0–100 的封号风险指数。
分数越高,像素美国警察的执法装备越离谱:
咖啡 + 甜甜圈巡逻 → 冒冷汗递巨型封号通知 → 高举半人高 BAN 锤 + 飞踢执法。

**除一次 IP 查询外,所有检测均在本地完成,不上传任何数据。**

## IP 查询

免费、无需 key、带 CORS 的三家依次兜底(第一家自带 `is_datacenter` 判定,后两家靠 AS 名称关键词):

1. [api.ipapi.is](https://ipapi.is)(约 1000 次/天)
2. [ipwho.is](https://ipwho.is)(约 10000 次/月)
3. [ipapi.co](https://ipapi.co)(约 1000 次/天)

三家全挂时输出「IP 查询失败。要么你断网了,要么你藏得真好。(+0)」,不影响其余检测。

## i18n

中英双语:`/zh/` 与 `/en/`,根路径按 `navigator.language` 自动分流,页头可手动切换。
文案集中在 [src/i18n.ts](src/i18n.ts)。

## 技术栈

- [Astro](https://astro.build) 5(纯静态输出)
- [Tailwind CSS](https://tailwindcss.com) 4(`@tailwindcss/vite`)
- 像素警察:纯 SVG,构建期由字符网格生成(与任何真实执法人员无关)

## 开发

```bash
npm install
npm run dev      # http://localhost:4321
npm run build    # 输出到 dist/
npm run preview
```

## 免责声明

本项目为 parody / satire,与 Anthropic、Claude 及任何真实人物均无关联。
所有「文件」「罪名」「判决」均为虚构玩梗,请勿当真。封号是为了你好。
