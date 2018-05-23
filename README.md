# AWS_serverless_Chapter6_pipeline
サーバレスアプリケーション開発ガイド Chapter６ーパイプライン作成


S3バケット作成
$ aws s3 mb s3://chapter6-lambda-function-src --region ap-northeast-1


クラウドフォーメーションロール作成
$ aws iam create-role --role-name chapter6-cloudformation-lambda-execution-role --assume-role-policy-document file://trustpolicy.json


クラウドフォーメーションロールにポリシー割当
$ aws iam put-role-policy --role-name chapter6-cloudformation-lambda-execution-role --policy-name chapter6-cloudformation-execution --policy-document file://permission.json


パイプラインIAMロール作成
$ aws iam create-role --role-name chapter6-codepipeline-role --assume-role-policy-document file://trustpolicy_codepipeline.json

ロールにポリシー割当
$ aws iam put-role-policy --role-name chapter6-codepipeline-role --policy-name chapter6-pipeline-service --policy-document file://permission_codepipeline.json


コードビルドIAMロール作成
$ aws iam create-role --role-name chapter6-codebuild-role --assume-role-policy-document file://trustpolicy_codebuild.json

ロールにポリシー割当
$ aws iam put-role-policy --role-name chapter6-codebuild-role --policy-name chapter6-codebuild-service --policy-document file://permission_codebuild.json

プロジェクト作成
aws codebuild create-project --cli-input-json file://project.json

パイプライン作成
$ aws codepipeline create-pipeline --cli-input-json file://pipeline.json

パイプラインスタート
$ aws codepipeline start-pipeline-execution --name chapter6-serverless-pipeline



結果：Buildステップで失敗
DOWNLOAD_SOURCE	Failed
[Container] 2018/05/23 05:18:37 Waiting for agent ping
[Container] 2018/05/23 05:18:41 Waiting for DOWNLOAD_SOURCE

>>> S3へのcodebuildIAMロールのアクセス権をフルアクセスに変更

