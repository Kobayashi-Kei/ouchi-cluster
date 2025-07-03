# webapp-helmfile-project

このプロジェクトは、Kubernetes 上でホストされる新しい Web アプリケーションのための Helmfile を使用した構成を提供します。以下に、プロジェクトの概要とセットアップ手順を示します。

## プロジェクトの構成

- `charts/webapp/Chart.yaml`: Helm チャートのメタデータを定義します。
- `charts/webapp/values.yaml`: デフォルトの値を定義し、デプロイメントやサービスの設定に使用される変数を含みます。
- `charts/webapp/templates/deployment.yaml`: Kubernetes のデプロイメントリソースを定義します。
- `charts/webapp/templates/service.yaml`: Kubernetes のサービスリソースを定義します。
- `charts/webapp/templates/ingress.yaml`: Kubernetes の Ingress リソースを定義します。
- `helmfile.yaml`: Helmfile の設定を定義します。
- `environments/production.yaml`: 本番環境用の設定を定義します。
- `environments/staging.yaml`: ステージング環境用の設定を定義します。
- `charts/container-registry/Chart.yaml`: プライベート Docker レジストリ用 Helm チャートのメタデータ。
- `charts/container-registry/values.yaml`: レジストリ用のデフォルト値。
- `charts/container-registry/templates/registry-deployment.yaml`: レジストリ用 Deployment リソース。
- `charts/container-registry/templates/registry-service.yaml`: レジストリ用 Service リソース。
- `charts/container-registry/templates/registry-ingress.yaml`: レジストリ用 Ingress リソース。
- `charts/container-registry/templates/registry-pvc.yaml`: レジストリ用永続ボリュームクレーム。
- `charts/nextcloud/Chart.yaml`: Nextcloud 用 Helm チャートのメタデータ。
- `charts/nextcloud/values.yaml`: Nextcloud 用のデフォルト値。
- `charts/nextcloud/templates/deployment.yaml`: Nextcloud 用 Deployment リソース。
- `charts/nextcloud/templates/service.yaml`: Nextcloud 用 Service リソース。
- `charts/nextcloud/templates/ingress.yaml`: Nextcloud 用 Ingress リソース。
- `charts/nextcloud/templates/pvc.yaml`: Nextcloud 用永続ボリュームクレーム。

※ registry 構築の参考: https://qiita.com/zknzfz/items/13d5d07ab5bb0feb1fd1

## セットアップ手順

1. **依存関係のインストール**:
   Helm と Helmfile をインストールしてください。

2. **チャートのデプロイ**:
   以下のコマンドを使用して、Helmfile を使用してチャート（webapp, container-registry, nextcloud）をデプロイします。

   ```zsh
   helmfile apply
   ```

3. **環境の設定**:
   `environments/production.yaml`または`environments/staging.yaml`を編集して、必要な設定を行います。

4. **アプリケーションへのアクセス**:
   デプロイ後、webapp・container-registry・nextcloud 用の Ingress リソースを使用して各サービスにアクセスできます。

## container-registry チャートの注意事項

- TLS 証明書（Secret）は事前に作成しておく必要があります。
- デフォルトの値や host 名は`charts/container-registry/values.yaml`で設定してください。
- registry の永続データは PVC で保持されます。

## nextcloud チャートの注意事項

- デフォルトで mariadb が有効になっています。必要に応じて`values.yaml`で設定を調整してください。
- Nextcloud の公式 Helm チャートの詳細は[公式リポジトリ](https://nextcloud.github.io/helm/)を参照してください。

## 注意事項

- 環境ごとに異なる設定が必要な場合は、適切な環境ファイルを編集してください。
- デフォルトの値は`charts/webapp/values.yaml`で設定されています。必要に応じて変更してください。

このプロジェクトを使用して、Kubernetes 上での Web アプリケーションのデプロイを簡素化できます。
