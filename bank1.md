# バンク1 - ゲームデータ

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
      <td>0x2598</td>
      <td>11</td>
      <td>0x2598</td>
      <td>6</td>
      <td>主人公名</td>
    </tr>
    <tr>
      <td>0x25F3</td>
      <td>3</td>
      <td>0x25EE</td>
      <td>3</td>
      <td>所持金</td>
    </tr>
    <tr>
      <td>0x25F6</td>
      <td>11</td>
      <td>0x25F1</td>
      <td>6</td>
      <td>ライバル名</td>
    </tr>
    <tr>
      <td>0x2602</td>
      <td>1</td>
      <td>0x25F8</td>
      <td>1</td>
      <td>ジムバッジ</td>
    </tr>
    <tr>
      <td>0x2605</td>
      <td>2</td>
      <td>0x25FB</td>
      <td>2</td>
      <td>トレーナーID</td>
    </tr>
    <tr>
      <td>0x2850</td>
      <td>2</td>
      <td>0x2846</td>
      <td>2</td>
      <td>コイン</td>
    </tr>
    <tr>
      <td>0x2CED</td>
      <td>5</td>
      <td>0x2CA0</td>
      <td>5</td>
      <td>プレイ時間</td>
    </tr>
    <tr>
      <td>0x2F2C</td>
      <td>404</td>
      <td>0x2ED5</td>
      <td>344</td>
      <td>手持ち</td>
    </tr>
    <tr>
      <td>0x3523</td>
      <td>1</td>
      <td>0x3594</td>
      <td>1</td>
      <td>チェックサム</td>
    </tr>
  </tbody>
</table>

## 💴 所持金

BCD形式で所持金が入っています。最大で999999円です。

## 🕰 プレイ時間

`255:00:00.00` まで記録できます。

プレイ時間が`255:00:00.00`になった場合、カウントストップフラグが1にセットされプレイ時間のカウントがストップします。

```
  Byte 0:  時
  Byte 1:  カウントストップフラグ
  Byte 2:  分
  Byte 3:  秒
  Byte 4:  フレーム
```

## 🎒 手持ち

オフセットは`0x2F2C`(日本版: `0x2ED5`)からのオフセットです。

ポケモンn は手持ちn匹目のポケモンを表します。(1が先頭, 6が最後尾)

手持ちポケモンが6匹に満たない場合、オフセット1の手持ちポケモンのIDの空き部分には`0xFF`が入ります。

Offset | Contents | Size(Byte)
--  | -- | --
  0 | 手持ちのポケモンの数 | 1
  1 | 手持ちポケモンのID x 6 | 6
  7 | 0xFF | 1
  8 | ポケモン1の[データ](./pkm.md) | 44
 52 | ポケモン2の[データ](./pkm.md) | 44
 96 | ポケモン3の[データ](./pkm.md) | 44
140 | ポケモン4の[データ](./pkm.md) | 44
184 | ポケモン5の[データ](./pkm.md) | 44
228 | ポケモン6の[データ](./pkm.md) | 44
272 | 親名 x 6 | *
272+* | ニックネーム x 6 | *

<details>
  <summary>親名とニックネームの詳細</summary>

  親名とニックネームのデータは、ポケモンデータとは離れた272バイト目以降に格納されています。

  英語版は1匹あたり11バイト、日本語版は6バイトです。
  よって上記の`*`は英語版は66バイト(11x6)、日本語版は36バイト(6x6)です。

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
      <td>272</td>
      <td>11</td>
      <td>272</td>
      <td>6</td>
      <td>ポケモン1の親名</td>
    </tr>
    <tr>
      <td>283</td>
      <td>11</td>
      <td>278</td>
      <td>6</td>
      <td>ポケモン2の親名</td>
    </tr>
    <tr>
      <td>294</td>
      <td>11</td>
      <td>284</td>
      <td>6</td>
      <td>ポケモン3の親名</td>
    </tr>
    <tr>
      <td>305</td>
      <td>11</td>
      <td>290</td>
      <td>6</td>
      <td>ポケモン4の親名</td>
    </tr>
    <tr>
      <td>316</td>
      <td>11</td>
      <td>296</td>
      <td>6</td>
      <td>ポケモン5の親名</td>
    </tr>
    <tr>
      <td>327</td>
      <td>11</td>
      <td>302</td>
      <td>6</td>
      <td>ポケモン6の親名</td>
    </tr>
    <tr>
      <td>338</td>
      <td>11</td>
      <td>308</td>
      <td>6</td>
      <td>ポケモン1のニックネーム</td>
    </tr>
    <tr>
      <td>349</td>
      <td>11</td>
      <td>314</td>
      <td>6</td>
      <td>ポケモン2のニックネーム</td>
    </tr>
    <tr>
      <td>360</td>
      <td>11</td>
      <td>320</td>
      <td>6</td>
      <td>ポケモン3のニックネーム</td>
    </tr>
    <tr>
      <td>371</td>
      <td>11</td>
      <td>326</td>
      <td>6</td>
      <td>ポケモン4のニックネーム</td>
    </tr>
    <tr>
      <td>382</td>
      <td>11</td>
      <td>332</td>
      <td>6</td>
      <td>ポケモン5のニックネーム</td>
    </tr>
    <tr>
      <td>393</td>
      <td>11</td>
      <td>338</td>
      <td>6</td>
      <td>ポケモン6のニックネーム</td>
    </tr>
  </tbody>
</table>

</details>

<details>
  <summary>Go言語の構造体で表した場合</summary>

```go
type Name = [6]uint8  // 海外版では [11]uint8

type Party struct {
  count   uint8
  species [7]uint8             // [ID, ID, ID, ID, ID, ID, 0xFF]
  datas   [6]PartyPokemonData  // 0xFF
  otnames [6]Name
  names   [6]Name
}
```
</details>
<br />

## ✅ チェックサム

[sav.md](./sav.md)を参照してください。

