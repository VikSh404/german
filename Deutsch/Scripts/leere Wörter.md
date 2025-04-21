
Wörter:
```dataviewjs
const folder = "Wörter"; // ← замени на путь к твоей папке
const emptyFiles = [];

const pages = dv.pages().where(p => p.file.path.startsWith(folder + "/"));
const promises = [];

for (const page of pages) {
    const filePath = page.file.path;
    const file = app.vault.getAbstractFileByPath(filePath);

    if (file && file.path.endsWith(".md")) {
        const promise = app.vault.read(file).then(content => {
            const cleaned = content
                .replace(/^---[\s\S]*?---/, '') // удаляет YAML-фронтматтер
                .replace(/\s+/g, '')            // удаляет пробелы и переносы строк
                .trim();
            if (cleaned.length === 0) {
                emptyFiles.push("[[" + filePath + "]]");
            }
        });
        promises.push(promise);
    }
}

await Promise.all(promises);
dv.list(emptyFiles);
```
