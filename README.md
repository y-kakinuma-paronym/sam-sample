# sam-sample

## コマンド

### ビルド

```
$ sam build
```

### 実行

```
$ sam local start-api
```

```
$ sam local invoke {実行関数名}
```

### デバッグ

vscodeの設定

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Attach to SAM CLI",
            "type": "node",
            "request": "attach",
            "address": "localhost",
            "port": 5858,
            // From the sam init example, it would be "${workspaceRoot}/hello-world"
            "localRoot": "${workspaceRoot}/{実行関数名}",
            "remoteRoot": "/var/task",
            "protocol": "inspector",
            "stopOnEntry": false
        }
    ]
}
```

デバッグ実行

```
$ sam local start-api --debug-port 5858 {実行関数名}
$ sam local invoke --debug-port 5858 {実行関数名}
```

### デプロイ

初回

```
$ sam deploy --guided
```

※次回以降のデプロイを簡略するために以下の設定で`y`を選ぶこと

```
Save arguments to configuration file [Y/n]: y
```

次回

```
$ sam build // 必ずビルドすること
$ sam deploy
```

### 削除

不要になったstackを削除

まずデプロイされているstackを確認する。

```
$ aws cloudformation list-stacks
```

cloudformationのstackを削除

```
$ aws cloudformation delete-stack --stack-name {StackName} --region ap-northeast-1
```