<link href="style.css" rel="stylesheet"></link>

# git コマンド覚書

<div style="text-align: right">2016/08/31 システム 谷口</div>


### エリア定義とコマンド
|リポジトリ|←|インデックス|←|ワークツリー|
|:--:|:--:|:--:|:--:|:--:|
|xxx.html|[`commit`](#commit)|xxx.html|[`add`](#commit)|xxx.html|


|リポジトリ|→|インデックス|→|ワークツリー<br />（変更後）|→|ワークツリー<br />（変更前）|
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|xxx.html|[`reset --soft HEAD^`](#softhard)<br /><br />[`reset --hard HEAD^`](#softhard)<br /><br />[`commit --amend`](#amend)|xxx.html|[`reset HEAD`](#reset)|xxx.html|[`checkout --`](#checkout)|xxx.html|

<br />

### <a name="checkout">変更されたファイルの内容を元に戻す（add前）
```
　　$ git checkout -- <file名>
```
ワークツリーで変更した、まだインデックス（stage）に登録されていないファイルを元に戻す。
<br />
<br />

### <a name="reset">add（stage）したファイルをインデックス（stage）から取り下げる -1（unstage）
```
　　$ git reset HEAD <file名>
```
インデックス（stage）から取り下げるだけなので、ファイルの変更そのものは残る。
add したものをまとめて取り下げる場合は、`$ git reset HEAD`とする。（HEADは省略可能）
<br />
<br />

### add（stage）したファイルをインデックス（stage）から取り下げる -2（unstage）
```
　　$ git rm --cached <file名>
```


`$ git rm`は、gitで管理されているファイルに対して`ファイルそのものを削除`し、管理対象からも除外する操作だが、
`--cached`オプションにより、ファイルを削除せずに管理対象からの除外だけを行える。
`--cached`オプションをつけ忘れるとファイルも削除されてしまうので、上の`reset`の方が安全。
<br />
<br />

### <a name="commit">add と commit をまとめて行う（コメント付き）
```
　　$ git commit -am "コメント"
```
<br />

### <a name="amend">直前の commit を修正する
```
　　$ git commit --amend -m "修正コメント"
```
直前のコミットをやり直したい場合は、`git commit --amend`を使用する。<br />
例：直前のコミットで、b.txt も含めたかった。<br />
　　直前のコミットコメントを修正したい。
<br />
<br />

### <a name="softhard">commit の取り消し
```
　　$ git reset --soft HEAD^
　　$ git reset --hard HEAD^
```

`git reset --soft`は、コミット時のワークツリーの内容ををのままで、コミットだけを取り消す。<br />
`git reset --hard`は、コミットを取り消した上で、ワークツリーの内容も書き換える。
`HEAD^`は直前のコミットを表す。
<br />
<br />

### commit の log 表示（コミットのハッシュ値を調べてサルベージしたい時）
```
　　$git relog
```
ローカルからリモートのブランチをチェックアウトした場合に detached HEAD状態になる。
detached HEAD状態で、コミットをした場合、どのブランチにも属さないコミットとなり
その後、別のブランチにチェックアウトしても通常の `$ git log` には表示されないという現象に陥る。
また、ブランチに属さないコミットなので、別ブランチではコミット内容が反映されていないため、
修正したはずのデータが修正されていないことになる。

その場合、 `$ git relog` で該当コミットのハッシュ値を調べてサルベージすることが可能である。
サルベージは、取り込みたいブランチから `$ git cherry-pick` する。

```
　　$ git cherry-pick <ハッシュ値>
```
<br />
