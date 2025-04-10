# 漆黒のtextarea

このシンプルなウェブページは、書くことに集中できる環境を提供します。ロードすると漆黒の画面に中央揃えされたテキストエリアが表示され、すぐに書き始めることができます。

## 特徴

* **漆黒の画面:** 背景が黒一色で、目に優しく集中力を高めます。
* **中央揃えの入力エリア:** 1行だけのときはほぼ画面中央に、複数行になると上下に余白を残しつつ広がります。
* **自動保存:** 入力が落ち着くと（3秒間入力がない場合）、内容が自動的にGitHubリポジトリの `contents.json` に保存されます。
* **LocalStorageとの連携:** 入力内容はLocalStorageにも保存され、ブラウザを閉じても保持されます。
* **リモートとローカルの同期:** ページロード時にGitHubから最新の `contents.json` を取得し、LocalStorageと比較して新しい方を採用します。
* **状態表示インジケーター:** 画面下部に現在の状態（入力待機、編集中、保存中、保存完了、エラー）が文字と色で表示されます。

## 使い方

1.  この `index.html` ファイルをブラウザで開きます。
2.  画面中央に表示されたテキストエリアに書き込みを開始します。
3.  入力が落ち着くと、自動的にGitHubリポジトリの `contents.json` に保存されます。
4.  ブラウザを閉じても、LocalStorageに内容が保存されているため、次回開いたときに続きから書き始めることができます。

## 事前準備

この機能を利用するためには、以下の準備が必要です。

1.  **GitHubアクセストークン:** GitHub APIへのアクセスに必要なアクセストークンを生成し、ブラウザのLocalStorageに `gh_token` というキーで保存してください。アクセストークンには `repo` スコープが必要です。
2.  **リポジトリURL:** 保存先のGitHubリポジトリのAPI URLをLocalStorageに `repo_url` というキーで保存してください。URLの形式は `https://api.github.com/repos/YOUR_USERNAME/YOUR_REPOSITORY` です。**`YOUR_USERNAME` と `YOUR_REPOSITORY` はあなたのリポジトリに合わせてください。**
3.  **`contents.json` ファイル:** 指定されたリポジトリのルートに `contents.json` という名前のファイルが存在している必要があります。このファイルは、少なくとも `{"text": "", "LastUpdated": null}` という基本的な構造を持っていることが推奨されます。

## LocalStorageへの設定例 (ブラウザの開発者コンソールにて)

GitHubアクセストークンを設定:

```javascript
localStorage.setItem('gh_token', 'YOUR_GITHUB_ACCESS_TOKEN');
```

リポジトリURLを設定 (あなたのリポジトリに合わせてください):

```javascript
localStorage.setItem('repo_url', '[https://api.github.com/repos/YOUR_USERNAME/YOUR_REPOSITORY](https://api.github.com/repos/YOUR_USERNAME/YOUR_REPOSITORY)');
```

## 注意事項

* GitHub APIの利用にはレート制限があります。頻繁な自動保存は制限に達する可能性があるため、3秒の遅延を設定しています。必要に応じて調整してください。
* エラーハンドリングは基本的なもののみ実装されています。より堅牢なアプリケーションにするためには、追加のエラー処理が必要です。
* このコードはクライアントサイドのJavaScriptで動作するため、アクセストークンをLocalStorageに保存することによるセキュリティ上のリスクを理解した上でご使用ください。

## 今後の開発

* より詳細な設定オプション（保存間隔の調整など）
* UIの改善
* オフラインサポート

---
