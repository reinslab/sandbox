#**gitflow における基本的な作業手順 第2版**

間違いがあれば修正して下さい。
sandboxで行うテストする場合は、別途upstreamのコマンドが必要です。

###事前準備
1.リモートリポジトリをクローンする

```
　　$ git cloen git@github.com:reinslab/xxxx.git
```
2.クローン直後のブランチの状態を確認する
```
　　$ git branch -a
```
実行結果
```
　　*develop
　　 remotes/origin/HEAD -> origin/develop
　　 remotes/origin/develop
　　 remotes/origin/master
　　 remotes/origin/product
```
3.upstream（追跡対象）を確認する
 ```
 　　$ git branch -vv
 ```
実行結果
 ```
 　　*develop xxxxxxx [origin/develop] xxxxxxx
```
4.git flow を初期化する
```
　　$ git flow init
```

###実際の開発の流れ
1.git flow をスタートする（featureA ブランチが自動的に作成される）
```
　　$ git flow feature start featureA
```
2.作成した feature ブランチで作業をする（開発・修正等）

3.インデックス（ステージング）する
```
　　$ git add xxxx
```
4.コミットする
```
　　$ git commit -m "何かコメント"
```
5.git flow をフィニッシュする（featureA ブランチは自動的に削除される）
```
　　$ git flow feature finish featureA
```
6.リモートの develop ブランチへプッシュする
```
　　$ git push
```
