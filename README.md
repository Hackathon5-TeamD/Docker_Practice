# Docker_Practice
Docker練習用

第３回ハッカソンで作成したTwitterAPI取得アプリです


起動手順
①から順に実行して下さい

①
```
./.cache_clear.sh
```

②
```
./.Database_clear.sh
```

③
```
docker-compose up -d --build
```

④
```
./.Database_clear.sh
```

⑤
```
./.migration.sh
```

以上でアプリが起動していますので、
ブラウザで、
```
localhost
```
で、ログイン画面
```
localhost/real/
```
で、Tweet取得画面になります。


終了処理
①
```
docker-compose down -v
```

②
```
docker rmi $(docker images -q)
```

③
```
docker system prune
```
⇨[y]

で、終了＆キャッシュクリアします。