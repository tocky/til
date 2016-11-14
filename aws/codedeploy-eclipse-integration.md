# Eclipse から CodeDeploy を使ったデプロイを実行

[AWS Toolkit for Eclipse](http://docs.aws.amazon.com/ja_jp/AWSToolkitEclipse/latest/GettingStartedGuide/Welcome.html) には CodeDeploy を使ったデプロイの実行がサポートされている。

Web アプリケーションとして作られているプロジェクトを右クリックして "Amazon Web Services" → "Deploy to AWS CodeDeploy" を選択することで、ウィザード形式によるデプロイを実行することができる。そして Eclipse からデプロイ実行する場合には AppSpec Template を選択することができ、これによって定義済みの `appspec.yml` および関連スクリプトをベースにデプロイを実行することができる。

## テンプレートの構成

テンプレートは次のような構成となる。

```
my-codedeploy-template
├── template
│   ├── appspec.yml
│   └── scripts
│       ├── application_start
│       └── application_stop
└── template.json
```

ルートディレクトリに `template.json` を配置、`template` ディレクトリ以下に `appspec.yml` やスクリプト類を配置する。

## `template.json` の記述

`template.json` に記述する内容はメタデータとして扱われる。さらに Eclipse のウィザードにて、パラメータ入力を促すこともできる。以下の例では `##HTTPD_SERIVCE_NAME##` というパラメータを定義している ([AWS Toolkit for Eclipse Integration with AWS CodeDeploy (Part 3) | AWS Developer Blog](https://aws.amazon.com/jp/blogs/developer/aws-toolkit-for-eclipse-integration-with-aws-codedeploy-part-3/) より引用)

```json
{
  "metadataVersion" : "1.0",
  "templateName" : "Stop Apache HTTP Server",
  "templateDescription" : "Stop Apache HTTP Server",
  "templateBasedir" : "/path/to/my-codedeploy-template/template",
  "isCustomTemplate" : true,
  "warFileExportLocationWithinDeploymentArchive" : "/application.war",
  "parameters" : [
    {
      "name" : "Apache HTTP service name",
      "type" : "STRING",
      "defaultValueAsString" : "httpd",
      "substitutionAnchorText" : "##HTTPD_SERVICE_NAME##",
      "constraints" : {
        "validationRegex" : "[\S]+"
      }
    }
  ]
}
```

スクリプト内では `substitutionAnchorText` で設定されているプレースホルダを使用できる。

```sh
#!/bin/bash

service ##HTTPD_SERVICE_NAME## stop
```

### テンプレートで使用できる項目

- `templateName`, `templateDescription` – テンプレートの名前と説明を指定する。
- `templateBasedir` – AppSpec ファイルおよびコマンドスクリプトが置かれているディレクトリを指定する。
- `isCustomTemplate` – `true` を設定することで、ユーザによって作成されたカスタムテンプレートであることを示し `templateBasedir` を絶対パスとして扱うことを知らせる。
- `warFileExportLocationWithinDeploymentArchive` – デプロイタスクが内部的に扱う WAR ファイル名を指定する。
- `parameters` – このテンプレートで設定可能な項目を列挙する。上述の例の場合には `##HTTPD_SERIVCE_NAME##` というパラメータのみを持っている。
    - ​`name` – このパラメータの名前
    - `type` – `STRING` もしくは `INTEGER`
    - `defaultValueAsString` – このパラメータのデフォルト値
    - `substitutionAnchorText` – パラメータに指定された値をテンプレート内のファイルに適用するため、識別子として定義するプレースホルダの名称。実行時にプラグインは識別子として記述されている箇所を実際の値に置き換える。
    - `constraints` – ユーザが入力したパラメータ値を検証するための制約。文字列の場合には `validationRegex` を設定でき、数値の場合には `minValue` と `maxValue` を設定できる。

_[AWS Toolkit for Eclipse Integration with AWS CodeDeploy (Part 3) | AWS Developer Blog](https://aws.amazon.com/jp/blogs/developer/aws-toolkit-for-eclipse-integration-with-aws-codedeploy-part-3/) を意訳_
