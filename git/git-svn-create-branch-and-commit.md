# git-svn 利用時に Subversion リポジトリにブランチを作成する

以下のコマンドはインストール済みとする。

* svn
* git
* git-svn

```
$ svn --version
svn, version 1.9.4 (r1740329)
   compiled Apr 28 2016, 01:15:57 on x86_64-apple-darwin15.4.0
$ git --version
git version 2.9.0
$ git svn --version
git-svn version 2.9.0 (svn 1.9.4)
```

恐らく `.git/config` では次のように Subversion リポジトリが登録されているはずである。

```
$ cat .git/config
...

[svn-remote "svn"]
  url = svn://example.com/foo
  fetch = trunk/path/to/myproject:refs/remotes/svn/trunk
  branches = branches/path/to/myproject/*:refs/remotes/svn/*

...
```

_初回のリポジトリ取得時 (`git svn clone`) では trunk の設定は入るものの branches は手動で追加してあげる必要がある。_

まずやるべきは **Subversion リポジトリ内で直接 trunk から branches 以下にコピーすること** である (Git の感覚に慣れすぎていると、ローカルの変更をリモートに適用しそうになる…)。次に参照先リモートブランチを変更し、そのブランチに対してローカルリソースを `dcommit` する。

```sh
$ svn cp svn://example.com/foo/trunk/path/to/myproject svn://example.com/foo/branches/path/to/myproject/myproject-branch 
$ git svn fetch
$ git rebase remotes/svn/myproject-branch
$ git svn dcommit --dry-run
$ git svn dcommit
```

## 参考

- [git-svn branching - Stack Overflow](http://stackoverflow.com/questions/2974016/git-svn-branching)
- [git svn - Git-svn: create & push a new branch/tag? - Stack Overflow](http://stackoverflow.com/questions/2490794/git-svn-create-push-a-new-branch-tag)
