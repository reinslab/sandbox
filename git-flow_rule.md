#**git flow 基本的な作業手順（簡易版）**

詳細は[redmine](http://redmine.wellco-reins.com　”redmine")で確認

###事前準備
1.リモートリポジトリをクローンする

```
　　$ git cloen git@github.com:reinslab/xxxx.git
```
2.ローカルに clone された作業ディレクトリに移動する
```
　　$cd xxxx
```

3.クローン直後のブランチの状態を確認する
```
　　$ git branch -a
```
実行結果
```
　　*develop
　　 remotes/origin/HEAD -> origin/develop
　　 remotes/origin/develop
　　 remotes/origin/master
　　 remotes/origin/production
```
4.production の upstream を設定する
```
　　$ git branch production remotes/origin/production
```
5.upstream（追跡対象）を確認する
 ```
 　　$ git branch -vv
 ```
実行結果
 ```
　　*develop 2734366 [origin/develop] xxxxx
　　 production 77d0fe3 [origin/production] xxxxxx
```
6.git flow を初期化する
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
