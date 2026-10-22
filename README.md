# Night Picker

星空・天体観測／夜景スポットを抽選し、星座図鑑、月齢・天文現象、地域別の天気予報も確認できる日本語Webアプリです。

## EdgeOneで公開する（初回のみ）

[![Deploy with EdgeOne Makers](https://cdnstatic.tencentcs.com/edgeone/pages/deploy.svg)](https://edgeone.ai/pages/new?repository-url=https%3A%2F%2Fgithub.com%2Ftontonmomo0712-a11y%2FNight-picker)

1. EdgeOne Makersで **Import Git Repository** を選択します。ZIPをアップロードする **Direct Upload** ではありません。
2. GitHubで **tontonmomo0712-a11y/Night-picker** を認証・選択します。
3. Production branchは **main**、Root directoryは **./**、Output directoryは **./（ルート）**、Build commandは**空欄**にします（HTMLのみでビルド不要）。
4. **Start Deployment** で公開します。
5. EdgeOneのProduction環境で **Auto Deploy** がオンになっていることを確認します。

GitHubの `main` ブランチの `index.html` を変更すると、EdgeOneが自動的に再公開します。公開後のURLはEdgeOne側で発行されます。

## 構成

- `index.html` ：アプリ全体（HTML / CSS / JavaScript）
- `README.md` ：公開と更新の手順

## 注意事項

- 所要時間は推定値です。道路の交通状況はGoogle Mapsなどで確認してください。
- 天気予報は外部APIの取得状況に依存します。
- 観測地の駐車可否や夜間利用条件、天候・安全情報は現地の最新情報を確認してください。
