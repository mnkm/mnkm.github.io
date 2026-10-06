# mnkm.github.io

このリポジトリは **旧 GitHub Pages（`https://mnkm.github.io/`）から新サイトへの転送用** です。
サイト本体は Cloudflare Pages に移行しました。

👉 **新しいサイト: https://mnkm.page/**

## 旧URLからの転送

GitHub Pages のカスタムドメイン設定により、旧URLへのアクセスは **301リダイレクト** で新サイトの同じパスへ転送されます。

| 旧URL | 新URL |
| --- | --- |
| `https://mnkm.github.io/` | `https://mnkm.page/` |
| `https://mnkm.github.io/<repo>/` | `https://mnkm.page/<repo>/` |

## 仕組み

- このリポジトリの **Settings → Pages → Custom domain** に `mnkm.page` を設定しています（`CNAME` ファイル）
- ユーザーサイトにカスタムドメインがあると、プロジェクトサイト（`mnkm.github.io/<repo>/`）も同じドメイン配下へ転送されます
- `mnkm.page` の DNS は Cloudflare を向いており、Worker がパスに応じて各 Cloudflare Pages プロジェクトへルーティングしています
- GitHub の Pages 設定画面に「DNS check unsuccessful」と表示されますが、DNS を Cloudflare に向けているためで想定どおりです

## ⚠️ 注意

以下を行うと、旧URLからの転送が止まります。

- このリポジトリを **削除・リネームしない**
- このリポジトリの **GitHub Pages を無効化しない**
- `CNAME` ファイル／Custom domain 設定を **削除・変更しない**
- 各プロジェクトリポジトリに **個別のカスタムドメインを設定しない**（そちらへ転送されてしまうため）

## 動作確認

```sh
curl -I https://mnkm.github.io/
curl -I https://mnkm.github.io/<repo>/
# → HTTP/2 301 / location: https://mnkm.page/... であればOK
```
