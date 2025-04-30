


```dataviewjs
(async () => {
  try {
    const pages = dv.pages('"Wörter"')
      .where(p => p.file.tags && p.file.tags.includes("#unreg"));

    dv.paragraph(`✅ Найдено файлов: ${pages.length}`);

    const rows = [];

    for (const p of pages) {
      const filePath = p.file.path;
      const file = app.vault.getAbstractFileByPath(filePath);

      if (!file || !(file instanceof obsidian.TFile)) {
        dv.paragraph(`⚠️ Не удалось получить файл: ${filePath}`);
        continue;
      }

      const content = await app.vault.read(file);
      const lines = content.split(/\r?\n/);
      const firstLine = lines.find(line => line.trim() !== "") || "(пусто)";
      const lastLine = lines[lines.length - 1] || "(пусто)";

      // ✅ Проверка количества вхождений "color:red" в первой строке
      const colorRedCount = (firstLine.match(/color:red/g) || []).length;

      if (colorRedCount <= 1) {
        rows.push([
          p.file.link,
          firstLine,
          lastLine,
          new Date(p.file.ctime).toLocaleDateString()
        ]);
      }
    }

    dv.table(["📄 Wort", "📝 Formen", "📝 Übersetzung", "🕒 Erstellt"], rows);
  } catch (e) {
    dv.paragraph(`❌ Ошибка: ${e.message}`);
    console.error(e);
  }
})();

```


```dataviewjs
(async () => {
  try {
    const pages = dv.pages('"Wörter"')
      .where(p => p.file.tags && p.file.tags.includes("#unreg"));

    dv.paragraph(`✅ Найдено файлов: ${pages.length}`);

    const rows = [];

    for (const p of pages) {
      const filePath = p.file.path;
      const file = app.vault.getAbstractFileByPath(filePath);

      if (!file || !(file instanceof obsidian.TFile)) {
        dv.paragraph(`⚠️ Не удалось получить файл: ${filePath}`);
        continue;
      }

      const content = await app.vault.read(file);
      const lines = content.split(/\r?\n/);

      // Ищем первую строку с двумя вхождениями "color:red"
      const firstLine = lines.find(line => (line.match(/color:red/g) || []).length === 2) || "(не найдено)";
      const lastLine = lines[lines.length - 1] || "(пусто)";

      if (firstLine !== "(не найдено)") {
        rows.push([
          p.file.link,
          firstLine,
          lastLine,
          new Date(p.file.ctime).toLocaleDateString()
        ]);
      }
    }

    dv.table(["📄 Wort", "📝 Formen", "📝 Übersetzung", "🕒 Erstellt"], rows);
  } catch (e) {
    dv.paragraph(`❌ Ошибка: ${e.message}`);
    console.error(e);
  }
})();

```

Verben:
```dataviewjs
(async () => {
  try {
    const pages = dv.pages('"Wörter"')
      .where(p => p.file.tags && p.file.tags.includes("#unreg"));

    dv.paragraph(`✅ Найдено файлов: ${pages.length}`);

    const rows = [];

    for (const p of pages) {
      const filePath = p.file.path;
      const file = app.vault.getAbstractFileByPath(filePath);

      // ✅ Проверка через obsidian.TFile
      if (!file || !(file instanceof obsidian.TFile)) {
        dv.paragraph(`⚠️ Не удалось получить файл: ${filePath}`);
        continue;
      }

      const content = await app.vault.read(file);
      const lines = content.split(/\r?\n/);
      const firstLine = lines.find(line => line.trim() !== "") || "(пусто)";
      const lastLine = lines[lines.length - 1] || "(пусто)";

      rows.push([
        p.file.link,
        firstLine,
        lastLine,
        new Date(p.file.ctime).toLocaleDateString()
      ]);
    }

    dv.table(["📄 Wort",  "📝 Formen", "📝 Übersetzung" , "🕒 Erstellt"], rows);
  } catch (e) {
    dv.paragraph(`❌ Ошибка: ${e.message}`);
    console.error(e);
  }
})();
```

