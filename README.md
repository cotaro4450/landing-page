# ✨ dfgc-proto ✨

DFGCオフィシャルサイトフェーズ１

## 利用環境

公開後にブログ投稿、コンテンツ追加を極力簡単に行えるようにして、メンテナンス性のよい構成を求める。

- ホスティング  Github Pages
- WEB制作    Gitローカル
- ブログ投稿    Forestry（ほかも検討）
- プレビューサイト    Netlify
- サイトジェネレータ    Hugo

## サイト公開準備

### 構成

![](/static/images/publish-flow-chart.webp)

#### Github構成
- ブランチは、preview → main → gh-pages の３段構成
- preview   ライターが投稿する場所。プレビュー用。
- main  ソースファイルの最新版がある場所
- gh-pages  ウェブ公開版。 `/public` のみ格納。

#### ツール
- Forestry　　ライターを登録。5名まで？ Adminアカウントをどれを使うか。
- Netlify   Adminアカウントをどれを使うか。

###  投稿フロー

- For ライター
    - ブログ、WEBページを書く。Netlifyでプレビューを見ながら編集
    - 公開できる状態になったらGithubでPRする
- For レビュワー
    - PRの内容を確認してマージ。mainブランチに適用
- 自動
    - main → gh-pages はGithub Actionで`/public`を自動生成

- For デザイナー
    - 新たに画像（svg, webb）をブランドアセットに載せるときは、WEB担当に言うか、自分で`/brand_asset`に置く。
- For 翻訳者
    - ウェブ担当が代理投稿。

### 備考
- 上記をより簡単に書いた投稿手順を、ハンドブックとしてDocsに書きたい。
    - For コントリビュータの項目で、For ライター、デザイナー、財務担当、ウェブ制作者　向けのガイド。
- PRはブラウザでボタンを押すだけで簡単だが、ライターとしては2ステップになり面倒。ここを自動PR処理すると下書きがPRされてしまうため、「下書き機能」を模索したい。
- ブログ投稿で画像を挿入する場合は、サイズ上限を決め、フォーマットをwebp限定にしたい。Github Pagesのストレージソフトリミットに達する懸念。pngで300KB〜数MBが次々とポストされるとサイトが止まる。→Docs
- 操作手順については画像を多く載せるため、Gitbookのガイドブックに書いてほしい。（For ユーザの項目）
- ブログは、オフィシャルアナウンスとファン投稿の２種類にし、テンプレートを分ける。投稿名義も分けるかどうかは検討。
    - オフィシャルアナウンスは、外向けのいわゆるメディアとしての発信。サービスリリース、計画進捗などの確定情報、定量的な情報を載せる。
    - 財務状況はオフィシャルでいいかな。
    - ファン投稿は、コミュニティやトークン、プロトコルの解説記事、Tips、コミュニティ状況を載せる。

### インフラ準備

1. defigeek.xyzリポジトリ作成
    - paruにリポジトリ書込み権限をほしい。理由は2.と4.を行うため。
2. 環境構築
    - 初回ミラーpush
    - 動作確認と調整
    - Github Pages設定
    - ツール連携（Netlify、Forestry）
    - Github Action設定 ＆ セキュリティキー登録
    - ※いまは個人レポで扱っていてProjectでの挙動がどうなるかは未知のため検証しながら。
3. DNS設定
    - Aレコード　`defigeek.xyz`と[GithubのIP](https://docs.github.com/ja/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site)
    - ALIAS　`www.defigeek.xyz`のリダイレクト
4. 正式リリース
    - カスタムドメイン設定
    - 切替タイミングは`/static`に`CNAME`を置いてPRマージするとき


## フェーズ2への書き残し
- テーマファイルの見直し
    - 多言語サポートを強化
    - フェーズ1運用後のセクション追加（FAQ, 募集など）の要望を反映
- デザイン
    - ブランドカラーのカラーパレット
    - CSSカスタマイズ
    - 新パレットでの素材作り
- より簡単に投稿できるツールを模索
    - For ライター、デザイナー、財務担当、ウェブ制作者、翻訳者
- Docsの統合
    - Gitbook, docsaurus, mdboook 系か Docslab, DigiDocs 系か
    - 選定にあたっては、Githubストレージ、Netlifyビルドのリミットを気にすること。
- インフラの検討
    - 分散型サービスの適用可能性、パフォーマンス、コストを調査
    - Fleek, IPFS, Storj
    - eth, hnsドメイン
    - ブランドアセットなどのファイル置き場。ヘッドレスCMSやChainsafeなど。

