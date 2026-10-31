# mnkm.github.io

旧 GitHub Pages(`https://mnkm.github.io/`)へのアクセスを、新しいサイト https://mnkm.page/ へ転送するためのリポジトリです。サイトの中身はありません。

## 転送先

旧 URL へのアクセスは新しいサイトの同じパスへ 301 で転送されます。

| 旧 URL | 新 URL |
| --- | --- |
| `https://mnkm.github.io/` | `https://mnkm.page/` |
| `https://mnkm.github.io/<repo>/` | `https://mnkm.page/<repo>/` |

## 仕組み

- このリポジトリの Settings → Pages → Custom domain に `mnkm.page` を設定しています(`CNAME` ファイル)。
- ユーザーサイト(このリポジトリ)にカスタムドメインがあると、GitHub はプロジェクトサイト(`mnkm.github.io/<repo>/`)へのアクセスも同じドメインへ転送します。
- `mnkm.page` の DNS は Cloudflare に向けてあり、Cloudflare の Worker がパスごとに各サイトへ振り分けます。
- DNS を Cloudflare に向けているため、GitHub の Pages の設定画面には「DNS check unsuccessful」と表示されます。転送には影響しません。

## 注意

次の操作をすると、旧 URL からの転送が止まります。

- このリポジトリを削除する、または名前を変える
- このリポジトリの GitHub Pages を無効にする
- `CNAME` ファイルや Custom domain の設定を消す、または変える
- ほかのリポジトリに個別のカスタムドメインを設定する(そのリポジトリのアクセスは、そのドメインへ転送されるようになります)

## 動作確認

```sh
curl -I https://mnkm.github.io/
curl -I https://mnkm.github.io/<repo>/
```

`HTTP/2 301` と `location: https://mnkm.page/...` が返れば、転送されています。
