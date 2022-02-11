# template-fastapi-docker
FastAPIをDockerを使って利用する時のテンプレート

```
mkdir new-project
cd new-project
git init
git clone https://github.com/xxx/xxx/[雛形].git .
git remote set-url origin　https://github.com/xxx/xxx/[新規].git
git fetch
git pull
git push origin
```

## イメージのbuild
```
docker-compose build
```


## poetryによるPython環境のsetup
Dockerコンテナの中で、poetry initコマンドの実行を行なっている。
依存パッケージとしてfastapiとuvicornを指定している。
poetryの定義ファイルを作成している。
```
docker-compose run --entprypoint "poetry init --name app-name --dependency fastapi --dependency uvicorn[standard]" app-name
```

インタラクティブなダイアログが始まるが、Author以外nで大丈夫。

## FastAPIのインストール
下記のコマンドで、installを実行。
```
docker-compose run --entrypoint "poetry install" app-name
```

新しくパッケージをインストールした際は、イメージの再ビルドを実行するだけで、pyproject.tomlに含まれているパッケージをインストールすることができる。
```
docker-compose build --no-cache
```
