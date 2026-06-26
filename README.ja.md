# StreamerVoiceOnly

ゲーム **Rust** 向けの [Oxide/uMod](https://umod.org/) プラグインです。ゲーム内のボイスチャットを制限し、**適切な権限を持つプレイヤー（配信者など）の声だけが聞こえる**ようにします。それ以外のプレイヤーの声はブロックされます。

- **作者:** jerky
- **バージョン:** 1.0.0

> 🇬🇧 English version: see [README.md](README.md)

## 仕組み

このプラグインは `OnPlayerVoice` イベントにフックします。プレイヤーが声を送信したとき:

- そのプレイヤーが `streamervoiceonly.use` 権限を**持っている**場合 → 声は通常どおり送信されます。
- 権限を**持っていない**場合 → ボイスデータがブロックされます（他のプレイヤーには声が聞こえません）。

配信者専用サーバーや、指定したプレイヤーだけにボイスチャットでの発言を許可し、他の全員をミュートしたいイベントなどに便利です。

## インストール

1. Rust サーバーで [Oxide/uMod](https://umod.org/) が動作していることを確認します。
2. `StreamerVoiceOnly.cs` をサーバーの `oxide/plugins/` ディレクトリにコピーします。
3. プラグインは自動的に読み込まれます（または、サーバーコンソールで `oxide.reload StreamerVoiceOnly` を実行します）。

## 権限

| 権限 | 説明 |
|---|---|
| `streamervoiceonly.use` | この権限を持つプレイヤーはボイスチャットを使用できます。 |

### 権限の付与

個別のプレイヤーに付与する場合:

```
oxide.grant user <steamID または 名前> streamervoiceonly.use
```

グループ全体（例: "streamer" グループ）に付与する場合:

```
oxide.group add streamer
oxide.grant group streamer streamervoiceonly.use
oxide.usergroup add <steamID または 名前> streamer
```

### 権限の剥奪

```
oxide.revoke user <steamID または 名前> streamervoiceonly.use
```

## 補足

- 権限を**持っていない**プレイヤーはサーバー全体でミュートされ、誰にも声が聞こえません。
- 設定ファイルは不要です。

## ライセンス

お使いの Rust サーバーで自由にご利用ください（現状のまま提供）。
