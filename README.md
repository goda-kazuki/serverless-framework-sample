# serverless-framework-sample

npmの初期化
`npm init`

serverlessのインストール
`npm install --save-dev serverless`

プロジェクト作成
`npx sls create --template aws-nodejs --name sample --path sample`

作成したプロジェクトに移動
`cd sample`

ローカルで実行
`npx sls invoke local -f hello`

レイヤーを追加する
```
mkdir layer
mkdir layer/nodejs
```

momentを追加
```
npm init
npm install moment
```

handler.jsにmomentを使うように指定
```
以下を追加
require('moment')
```

実行(失敗する)
`npx sls invoke local -f hello`

serverless.ymlに以下を追加
```
functions:
  hello:
    handler: handler.hello
    layers:
      - { Ref: SampleLambdaLayer }

layers:
  Sample:
    path: layer
    description: my sample layer
    compatibleRuntimes:
      - nodejs12.x
```

実行(失敗する)
`npx sls invoke local -f hello`

--dockerオプションを追加して実行(成功する)
`npx sls invoke local -f hello --docker`
