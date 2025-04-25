# Gitとは？

<a href = "https://qiita.com/marchin_1989/items/2ec01553e907f3a9e6bb">Git</a>

## Gitの基本的な使い方

Gitはローカルリポジトリとリモートレポジトリの2つがある。ローカルリポジトリは自分のローカルPCなどの端末に作成するものであるのに対し、リモートリポジトリは自分以外のユーザーと共有することを前提にするため、基本的にはサーバーやGithubなどに作成する。
自分のみで履歴管理をGitで行いたい場合は、リモートリポジトリはなくてもよい。ローカルリポジトリでの履歴管理はAddとCommitの二種類のコマンドで行う。リモートリポジトリへ履歴をローカルリポジトリから反映する場合はPushを使う。
AddはGitオブジェクトのBlobオブジェクトを生成することに等しく、CommitはTreeオブジェクトを生成することに等しい。

# Gitの初期設定
Gitをインストールしたら，まずは次の内容くらいは初期設定をしておくとよいです．Git for Windowsに同梱されているGit Bashを起動して，以下の内容でコマンドを実行します．
https://github.com/kaityo256/github/blob/main/basics/README.md

```
git config --global user.name 'username'
git config --global user.email 'username@example.com'
git config --global core.editor 'code --wait'
git config --global merge.tool 'code --wait "$MERGED"'
git config --global push.default simple
git config --global pull.rebase false
git config --global core.quotepath false
```

# ローカルリポジトリとリモートリポジトリの紐づけ

```{git}
git remote add (remote repository name) (remote repository URL)
```

# originとは

リモートリポジトリのアクセス先に対してGitがデフォルトでつける名前です。以下でOriginがどのアクセス先を参照しているかを確認することができます。

```{git}
git remote -v
```

つまり、git push origin masterならOrignで指定されたリモートレポジトリのアクセス先のMasterブランチに対してPushするという意味になります。
ちなみに実際Originとアクセス先の記載は.gitフォルダ内にあるconfigファイル内にあります。

アクセスするリモートレポジトリ先を変更した場合は以下のようにします。

```{git}
git remote set-url origin (new URL)
```

逆にリポジトリ名をOriginから変更した場合は以下のようにします。

```{git}
git remote rename origin (new repository name)
```

# clone
How to download files from a remote repository to a local repository

```
git clone <remote repository>
```
## clone a remote private repository 
```
git clone https://{user_name}@github.com/{user_name}/
```

# Gitの管理対象から特定のファイルを除外する（.gitignore）

https://www-creators.com/archives/1662

https://bayashita.com/p/entry/show/37

https://www.delftstack.com/ja/howto/powershell/edit-a-text-file-on-the-console-using-powershell/


特定のファイルやフォルダをGitの管理下に置きたくない場合は.gitignoreで指定する。

1 まず.gitignoreファイルを作成。ドットが先頭につくファイルやフォルダは隠しファイル・フォルダを意味している。作成はVIMを使って行う。WindowsではVIMがデフォルトでは入ってないのでインストールしてCMDから利用できるように設定を行う。

<a href = "https://www.jcsc.co.jp/tech_blog/archives/28">テキストエディタ「Vim」を、Windowsでも使う方法</a>

<a href = "https://www-creators.com/archives/1488">Vim commands </a>

## 外部の git リポジトリを、自分の git リポジトリのサブディレクトリとして登録し、特定の commit を参照する(既存のローカルレポジトリにリモートレポジトリをCloneする)
```
git submodule add <remote repository URL>
git status
git diff --cached
git commit -m "comments"
git show
```

# Push
```
git push (remote repo. name) (remote branch name)
```

## the step only for 1st push
```
git remote add origin git@github.com:ユーザー名/リポジトリ名.git
```

## 更新するリモートブランチ名を明示的に指定して push する
```
// ローカルブランチ「develop」を、リモートブランチ「master」に push 
git push origin develop:master
```

# Merge
How to merge a branch to another branch
Gitでは、原則としてmainブランチで作業しない。自分がこれから行う作業に対応したブランチを用意し(ブランチを切る、と呼ぶことが多い)、そのブランチ上で作業を行う。作業が一段落したら、ブランチで作業した内容をmainブランチに取り込みたくなる。このように、片方のブランチの修正をもう一つのブランチに取り込むことを マージ(merge) と呼ぶ。
ローカルリポジトリにおいて最新の状態にしたmasterブランチに、developブランチの内容を取り込みます。

```
git merge develop
git push origin master
```
## Two kinds of merges
- Fast-Forward marge = merge from a branch to a main branch when there is no new commits on a main branch 
- Non Fast-Forward marge = merge from a branch to a main branch when there is new commits on a main branch. If the commits on the branch and the ones on the main brach are contradictory, that is called 'conflict' and you cannot merge them.

## merge a develop branch into a master branch
```
git checkout master 
git merge develop
```

# fetch
How to see any updates on a remote repository

```
git fetch origin (branch name)
```

# ローカルgitリポジトリでリモートのリポジトリURL確認方法
```
git config --get remote.origin.url
```

# Fork
fork（派生）とはある時点のリポジトリをベースとして、GitHub上に別のリポジトリとして作成することです。
一般的にフォークは、他のユーザのプロジェクトへの変更を提案するため、あるいは他のユーザのプロジェクトを自分のアイディアの出発点として活用するために使用します。
https://style.potepan.com/articles/31067.html

# Pull
pullを実行するとリモートリポジトリの履歴を取得することができます。git fetch、git mergeを同時に行うコマンドです。

```
git pull origin (branch name)
```
## エラーがあって元に戻したい時
```git
git reset --hard HEAD
```

# Pull request
簡単に言うと、開発者のローカルリポジトリでの変更を他の開発者に通知する機能です。プルリクエストは次のような機能を提供します。
https://backlog.com/ja/git-tutorial/pull-request/01/

- 機能追加や改修など、作業内容をレビュー・マージ担当者やその他関係者に通知します。
- ソースコードの変更箇所をわかりやすく表示します。
- ソースコードに関するコミュニケーションの場を提供します。


# Commit
How to update any files in a local repository
- step 1: (Staging) インデックスにコミットされるスナップショットを作る
```
git add <the name of the file>
```

- step 2: 現在の状態を見る
```
git status
```

- step 3: コミットを作ろう。
```
git commit -m <comments>
```
すると、デフォルトエディタ(本講義の設定ではvim)が起動し、以下のような画面が表示される。

- step 4: コミットメッセージを書く

最初のコミットメッセージはinitial commitとすることが多い。なお、#で始まる行はコミットメッセージには含まれない。コミットメッセージを入力し、ファイルを保存してエディタを終了するとコミットが実行される。

Normal mode on vm;
```
zz 
```

- step 5: 過去のコミットを見てみよう。
```
git log
```

- step 6: 修正をコミット

Git Bashでカレントディレクトリが(target folder)である状態から、
```
code .
```
を実行すると、このディレクトリをVS Codeで開くことができる。

# git add を取り消す

全てのファイルを取り消し
```
git rm --cached -r 
```

特定のファイルのみ取り消し
```
git rm --cached -r file_name
```

### Gitリポジトリからファイルを削除する
３パターンある
- 1 リポジトリから削除、かつ、ディレクトリから削除（i.e. 完全に削除）
- 2 リポジトリから削除、かつ、ディレクトリには残す
- 3 リポジトリには残す、かつ、ディレクトリから削除（あんまりないかも）

```
git rm FILENAME           ## 1.の場合
git rm --cached FILENAME  ## 2.の場合
rm FILENAME               ## 3.の場合
```

1.の場合については、以下と同じ
```
rm FILENAME       ## ファイルが deleted になる
git add FILENAME  ## deletedなことがステージされる
```
# regular expression
https://kledgeb.blogspot.com/2015/04/ubuntu-git-165-git-rm.html

# すでに存在するプロジェクトのディレクトリをGit管理にする方法

- step 1:存在するプロジェクトのディレクトリへ移動

```
 cd <the directory path in which the project is>
```

- step 2: Gitの初期化
```
git init
git commit -m 'initial commit'
```

すると、ディレクトリ直下に.gitというディレクトリが作られる。Gitの管理情報は全てこのディレクトリに格納される。

# Branch
Branch = コミットについたラベル。プロジェクトをGitで初期化した場合、デフォルトでmainというブランチが用意される
HEAD =  ブランチが複数あると、「今自分がどのブランチを見ているのか」という情報が必要だ。それを指すのが「HEAD」である。Gitはデフォルトでmainブランチが作られ、「HEAD」はmainを指している。
detached HEAD = 通常HEADはブランチを経由してコミットを指しているが、操作によってはHEADが直接コミットを指す場合がある。これを「detached HEAD状態」と呼ぶ。

## ブランチを作成する

```
git branch <branchname>
git branch
```

## ブランチを切り替える
さて、新しく作成したissue1ブランチにコミットを追加していくには、issue1ブランチをチェックアウトする必要があります。
```
git checkout <to branch>
```

## ブランチをマージする

```
git merge <branchname that you want to merge with the current branch>
```

## ブランチを削除する

```
git branch -d <branchname>
```

## 自分が今いるブランチを確認するコマンド
```
git branch --contains
```

## Git tag

<a href = "https://prograshi.com/general/git/all-of-git-tag-command/">git tag</a>

## リモートブランチを削除する
https://qiita.com/yuu_ta/items/519ea47ac2c1ded032d9
```
git push --delete origin branch_name
```

## gitのローカルリポジトリを削除する方法
```
git rm -rf .git
```
# mv
## rename a file in a local repository
```
git mv (name before renamed) (name after renamed)
```

## rename a folder in a local repository
```
git mv folderBefore/ folderAfter/
```

## rename a remote repository with a local git command
```
git remote rename  <old_name> <new_name>
```

# Commit hash
Gitでは歴史をコミットで管理しており、コミットは「コミットされた時点でのプロジェクトのスナップショット」を表す。そのコミットを区別する一意な識別子がコミットハッシュである。コミットハッシュの上位7桁しか表示されなかったが、実際には40桁ある

# ブランチの命名規則
https://qiita.com/c6tower/items/fe2aa4ecb78bef69928f

# Pythonで作ったコマンドをGitHub経由でpipインストール可能にする
https://dev.classmethod.jp/articles/pip-install-via-github-command/

# cheat sheet
https://qiita.com/2m1tsu3/items/6d49374230afab251337

# error handling
## error: the following file has staged content different from both the file and the HEAD:
https://qiita.com/baby-0105/items/3a819d25c905dc8bcb19

## fatal: Not a valid object name: 'master'.
https://qiita.com/takuma-jpn/items/fe205ff59cfa10746aa8

## warning: LF will be replaced by CRLF in
https://penpen-dev.com/blog/warning-lf-willbe/

## error: src refspec develop does not match any
https://www-creators.com/archives/1472

# .gitディレクトリを理解する

gitを利用するには最初にgit initで初期化する。これを行うと、そのフォルダ内がGitの管理対象になる。その際にバックエンドでは.gitフォルダが生成されている。この.gitフォルダにはGitを管理する上で必要なパラメータ等が記録されており、Gitコマンドを利用したときに、そのパラメータが参照されている。以下はフォルダ内にあるファイルやフォルダの意味合いである。

<a href = "https://qiita.com/tatane616/items/dbad66179754be57d2e2">.gitの中身</a>

## HEAD

現在参照しているリモートリポジトリのブランチが記載されている。例えばリモートレポジトリのDevelopブランチを参照しているなら「ref: refs/heads/develop」のように記載されている。ブランチを切り替えるGitコマンドはここの記載を変更することに等しい

```{git}
git checkout (新たに参照したブランチ名)
```

ちなみに、ブランチを新規に作成しつつ、そのブランチを新たな参照先にしたい場合は-b オプションをつかう

```{git}
git checkout -b (新たに参照したブランチ名)
```

## Config

リモートレポジトリ名とアクセス先の紐づけ情報などが記載されている他、さまざまな設定のパラメータが保存されている。

## Description

GitWeb(gitのデフォルトのWebUI)で使われる

## hooks

Gitコマンドの内容を編集することができる。Gitコマンドは.sampleファイルにそれぞれ記述されている。これらのファイルはシェルスクリプトやPerl,Ruby,Pythonなど複数の言語で記述することができる。

<a href = "https://git-scm.com/book/ja/v2/Git-%E3%81%AE%E3%82%AB%E3%82%B9%E3%82%BF%E3%83%9E%E3%82%A4%E3%82%BA-Git-%E3%83%95%E3%83%83%E3%82%AF"> git hooks</a>

<a href = "https://qiita.com/nicco_mirai/items/b1818efd4d9516b42e40"> Git hookをPythonで記載する方法</a>

## info

リポジトリに対する追加情報で、excludeファイルなどを含む。Excludeファイルにはgitで対象としないフォルダやファイルの情報が記載されている

## objects

gitのオブジェクトが保存されている。フォルダの中を見ると、複数のフォルダがある。さらに各フォルダをみると、一つまたは複数のファイルが保存されている。これら一つ一つがGitオブジェクトと呼ばれる。Gitオブジェクトのファイル名は40文字のハッシュで先頭の2文字がサブフォルダ名、残りの38文字がファイル名という構成になっている。ハッシュはSHA1ハッシュ。

<a href = "https://qiita.com/nkshigeru/items/eb2b6f758c2707757738">Gitオブジェクトについて</a>

## refs

Gitの各参照先が保存されている場所

