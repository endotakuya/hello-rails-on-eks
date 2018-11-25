# EKSでRailsアプリケーションを動かすサンプルリポジトリ

## 事前準備

1. Railsアプリケーションの作成
2. Dockernize
3. 必要なコマンド類のインストール
    - aws cli（あった方が楽）
    - kubectl
    - kubectx（クラスタの変更が容易になる）

## 大まかな作業手順

公式ドキュメントに沿って進めます。  
`ステップ 4: ゲストブックアプリケーションを起動する` の手前までは、同じ作業でOKです。  
https://docs.aws.amazon.com/ja_jp/eks/latest/userguide/getting-started.html

1. Amazon EKS サービスロールの作成
2. Amazon EKS クラスター VPC の作成
3. Amazon EKS ワーカーノードの起動 & 設定
4. Rails アプリケーションのデプロイ

※ EKS は、現在東京リージョンが使えない。ので、バージニア北部を使用。

## Rails アプリケーションのデプロイ

### Docker イメージを Dockerhub へ Push

```bash
$ docker login
$ docker image build -t enta0701/hello-rails:v1 -f .docker/app/Dockerfile .
$ docker image push enta0701/hello-rails:v1
```

### デプロイ

```bash
$ ku apply -f .k8s/hello-rails.yaml
```

### 削除

```
$ ku delete -f .k8s/hello-rails.yaml
```