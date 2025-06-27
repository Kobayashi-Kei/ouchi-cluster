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

## セットアップ手順

1. **依存関係のインストール**:
   Helm と Helmfile をインストールしてください。

2. **チャートのデプロイ**:
   以下のコマンドを使用して、Helmfile を使用してチャートをデプロイします。

   ```
   helmfile apply
   ```

3. **環境の設定**:
   `environments/production.yaml`または`environments/staging.yaml`を編集して、必要な設定を行います。

4. **アプリケーションへのアクセス**:
   デプロイ後、Ingress リソースを使用してアプリケーションにアクセスできます。

## 注意事項

- 環境ごとに異なる設定が必要な場合は、適切な環境ファイルを編集してください。
- デフォルトの値は`charts/webapp/values.yaml`で設定されています。必要に応じて変更してください。

このプロジェクトを使用して、Kubernetes 上での Web アプリケーションのデプロイを簡素化できます。
