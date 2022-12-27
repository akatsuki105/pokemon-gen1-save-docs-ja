# レポートのデータ構造(第1世代)

オフセットは、`.sav`ファイルの先頭からのオフセットです。

## 🏦 バンク構造

<table>
  <tbody>
    <tr>
      <th>バンク</th>
      <th>オフセット</th>
      <th>内容(En)</th>
      <th>内容(Ja)</th>
    </tr>
    <tr>
      <td>0</td>
      <td>0x0000</td>
      <td colspan="2">殿堂入り、スプライトデータなど</td>
    </tr>
    <tr>
      <td>1</td>
      <td>0x2000</td>
      <td colspan="2"><a href="./bank1.md">ゲームデータ</a></td>
    </tr>
    <tr>
      <td>2</td>
      <td>0x4000</td>
      <td><a href="./bank2-3.md">PCボックス1~6</a></td>
      <td><a href="./bank2-3.md">PCボックス1~4</a></td>
    </tr>
    <tr>
      <td>3</td>
      <td>0x6000</td>
      <td><a href="./bank2-3.md">PCボックス7~12</a></td>
      <td><a href="./bank2-3.md">PCボックス5~8</a></td>
    </tr>
  </tbody>
</table>

## ✅ チェックサム

チェックサムが合っていないセーブデータは不正なデータとみなされ読み込んでくれません。

チェックサムは8bitで、計算は次のように行います。

```go
const (
  start = 0x2598  // 日本語・英語版共通
  end   = 0x3593  // 英語版は 0x3521
  dst   = 0x3594  // 英語版は 0x3523
)

  checksum := uint8(255)
  for (ofs := start; ofs < end; ofs++) {
    checksum -= getByte(sav, ofs)
  }
  sav[dst] = checksum
```

## 外部リンク

- [Save data structure (Generation I)](https://bulbapedia.bulbagarden.net/wiki/Save_data_structure_(Generation_I))
