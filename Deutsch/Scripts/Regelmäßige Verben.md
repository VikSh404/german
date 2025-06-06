
Verben:
```dataviewjs
(async () => {
  try {
    const pages = dv.pages('"Wörter"')
      .where(p => p.file.tags && p.file.tags.includes("#reg"));

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
        lastLine,
        new Date(p.file.ctime).toLocaleDateString()
      ]);
    }

    dv.table(["📄 Wort", "📝 Übersetzung" , "🕒 Erstellt"], rows);
  } catch (e) {
    dv.paragraph(`❌ Ошибка: ${e.message}`);
    console.error(e);
  }
})();
```


