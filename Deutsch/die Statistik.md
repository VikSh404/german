
```dataviewjs
let count = dv.pages('"Wörter"').length;
dv.paragraph(`📄 die Anzahl der Wörter: **${count}**`);
```
---
```dataviewjs

let count = dv.pages('"Wörter"')
  .where(p => p.file.tags && p.file.tags.includes("#unreg"))
  .length;

dv.paragraph(`📄 Unregelmäßige Verben: **${count}**`);

```
---
```dataviewjs

let count = dv.pages('"Wörter"')
  .where(p => p.file.tags && p.file.tags.includes("#reg"))
  .length;

dv.paragraph(`📄 Regelmäßige Verben: **${count}**`);

```
---
```dataviewjs

let count = dv.pages('"Wörter"')
  .where(p => p.file.tags && p.file.tags.includes("#adverb"))
  .length;

dv.paragraph(`📄 Adverben: **${count}**`);

```
---

```dataviewjs

let count = dv.pages('"Wörter"')
  .where(p => p.file.tags && p.file.tags.includes("#Adjektiv"))
  .length;

dv.paragraph(`📄 Adjektive: **${count}**`);

```
---

```dataviewjs
let pages = dv.pages('"Wörter"')
  .where(p => p.file.tags && p.file.tags.includes("#nomen"));

let derCount = pages.filter(p => p.file.name.toLowerCase().startsWith("der ")).length;
let dieCount = pages.filter(p => p.file.name.toLowerCase().startsWith("die ")).length;
let dasCount = pages.filter(p => p.file.name.toLowerCase().startsWith("das ")).length;

dv.paragraph(`📄 **Nomen**: ${pages.length}  
🟦 der: ${derCount} 
🟪 die: ${dieCount}  
🟨 das: ${dasCount}`);
```
---
```dataviewjs
const pages = dv.pages('"Wörter"')
  .where(p => p.file.tags && p.file.tags.includes("#nomen"))
  .sort(p => p.file.ctime, 'desc') // сортируем по дате создания
  .slice(0, 50); // берём только 50

dv.table(["📄 Wort", "🕒 Erstellt"], 
  pages.map(p => [p.file.link, p.file.ctime.toLocaleString()]));
```

