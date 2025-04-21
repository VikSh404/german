```dataviewjs
const folderPath = 'Wörter'; // 🔁 Укажи свою папку здесь
const unresolvedLinks = new Set();

for (let page of dv.pages(`"${folderPath}"`)) {
    for (let link of page.file.outlinks) {
        const fullPath = `${folderPath}/${link.path}`;
        if (!app.metadataCache.getFirstLinkpathDest(link.path, page.file.path)) {
            unresolvedLinks.add(fullPath);
        }
    }
}

const links = Array.from(unresolvedLinks).map(link => `[[${link}]]`);
dv.list(links);
```
