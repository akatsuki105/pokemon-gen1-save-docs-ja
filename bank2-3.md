# バンク2-3 - PCバッファ

バンク2-3はPCについてのデータ(PCバッファ)を格納しています。

オフセットは、`.sav`ファイルの先頭からのオフセットです。

<table>
  <tbody>
    <tr>
      <td colspan="2">
        <b>English</b>
      </td>
      <td colspan="2">
        <b>Japanese</b>
      </td>
      <td></td>
    </tr>
    <tr>
      <th>Offset</th>
      <th>Size</th>
      <th>Offset</th>
      <th>Size</th>
      <th>Contents</th>
    </tr>
    <tr>
      <td>0x4000</td>
      <td>1122</td>
      <td>0x4000</td>
      <td>1382</td>
      <td>ボックス1のデータ</td>
    </tr>
    <tr>
      <td>0x4462</td>
      <td>1122</td>
      <td>0x4566</td>
      <td>1382</td>
      <td>ボックス2のデータ</td>
    </tr>
    <tr>
      <td>0x48C4</td>
      <td>1122</td>
      <td>0x4ACC</td>
      <td>1382</td>
      <td>ボックス3のデータ</td>
    </tr>
    <tr>
      <td>0x4D26</td>
      <td>1122</td>
      <td>0x5032</td>
      <td>1382</td>
      <td>ボックス4のデータ</td>
    </tr>
    <tr>
      <td>0x5188</td>
      <td>1122</td>
      <td>0x6000</td>
      <td>1382</td>
      <td>ボックス5のデータ</td>
    </tr>
    <tr>
      <td>0x55EA</td>
      <td>1122</td>
      <td>0x6566</td>
      <td>1382</td>
      <td>ボックス6のデータ</td>
    </tr>
    <tr>
      <td>0x6000</td>
      <td>1122</td>
      <td>0x6ACC</td>
      <td>1382</td>
      <td>ボックス7のデータ</td>
    </tr>
    <tr>
      <td>0x6462</td>
      <td>1122</td>
      <td>0x7032</td>
      <td>1382</td>
      <td>ボックス8のデータ</td>
    </tr>
    <tr>
      <td>0x68C4</td>
      <td>1122</td>
      <td colspan="2">N/A</td>
      <td>ボックス9のデータ</td>
    </tr>
    <tr>
      <td>0x6D26</td>
      <td>1122</td>
      <td colspan="2">N/A</td>
      <td>ボックス10のデータ</td>
    </tr>
    <tr>
      <td>0x7188</td>
      <td>1122</td>
      <td colspan="2">N/A</td>
      <td>ボックス11のデータ</td>
    </tr>
    <tr>
      <td>0x75EA</td>
      <td>1122</td>
      <td colspan="2">N/A</td>
      <td>ボックス12のデータ</td>
    </tr>
  </tbody>
</table>

## 💻 ボックスデータ

英語版は1つのボックスあたり20匹、日本語版は30匹格納できます。

ポケモンn はボックスn匹目のポケモンを表します。(ポケモン1が先頭)

ボックス内のポケモンが30匹(英語版は20)に満たない場合、オフセット1の`ボックス内のポケモンのID`の空き部分には`0xFF`が入ります。

**日本語版**

Offset | Contents | Size(Byte)
--  | -- | --
   0 | ボックス内のポケモンの数 | 1
   1 | ボックス内のポケモンのID x 30 | 30
  31 | 0xFF | 1
  32 | ポケモン1の[データ](./pkm.md) | 33
  66 | ポケモン2の[データ](./pkm.md) | 33
 989 | ポケモン30の[データ](./pkm.md) | 33
1022 | 親名 x 30 | 180
1202 | ニックネーム x 30 | 180

**英語版**

Offset | Contents | Size(Byte)
--  | -- | --
  0 | ボックス内のポケモンの数 | 1
  1 | ボックス内のポケモンのID x 20 | 20
 21 | 0xFF | 1
 22 | ポケモン1の[データ](./pkm.md) | 33
 55 | ポケモン2の[データ](./pkm.md) | 33
649 | ポケモン20の[データ](./pkm.md) | 33
682 | 親名 x 20 | 220
902 | ニックネーム x 20 | 220

親名とニックネームのデータは、ポケモンデータとは離れた1022バイト目(682バイト目)以降に格納されています。日本語版は1匹あたり6バイト、英語版は11バイトです。

<details>
  <summary>Go言語の構造体で表した場合</summary>

  ```go
  type Name = [6]uint8  // 英語版では [11]uint8
  type LEN = 30         // 英語版では1ボックス20匹なので LEN=20

  type PCBox struct {
    count   uint8
    species [LEN+1]uint8         // [ID, ID, ID, ID, ID, ID, ..., 0xFF]
    datas   [LEN]BoxPokemonData  // 0xFF
    otnames [LEN]Name
    names   [LEN]Name
  }
  ```
</details>
