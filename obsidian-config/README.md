# Obsidian Config (참고용)

이 폴더의 파일들은 **본인 vault의 `.obsidian/` 폴더에 그대로 복사**해도 되고, plugin GUI 설정창에서 같은 값을 입력해도 된다. (`docs/02-plugin-config.md` 참조)

## 복사 방법 (선택)

```bash
# 본인 vault의 .obsidian 폴더가 있다면
cp community-plugins.json ~/Obsidian/MyVault/.obsidian/
cp core-plugins.json ~/Obsidian/MyVault/.obsidian/
cp templates.json ~/Obsidian/MyVault/.obsidian/
cp daily-notes.json ~/Obsidian/MyVault/.obsidian/
cp -R plugins/periodic-notes ~/Obsidian/MyVault/.obsidian/plugins/
cp -R plugins/templater-obsidian ~/Obsidian/MyVault/.obsidian/plugins/
```

복사 후 Obsidian 재시작.

> ⚠️ Plugin 본체(`main.js` 등)는 Obsidian이 자동 다운로드. 여기 있는 건 **설정값만**.
