---
title: Gitの設定
teaching: 5
exercises: 0
---

::::::::::::::::::::::::::::::::::::::: objectives

- コンピュータで初めて `git` を使うための設定が出来るようになりましょう。
- `--global` 設定フラグの意味を理解しましょう。

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Git を使うために必要な設定は何ですか？

::::::::::::::::::::::::::::::::::::::::::::::::::

Git を新しいパソコンで初めて使う場合、いくつかの設定を変更しなければなりません。 Git を始めるにあたって、私達が変更する設定をいくつか表記します：

- 名前とメールアドレス、
- 使用したいテキストエディタ、
- 以上の設定をグローバル設定として使う（つまり、全てのプロジェクトに反映させる）。

コマンドラインでは、Git コマンドは `git <動詞> <オプション>` と入力します。ここでの「動詞」は、Git に何をさせたいのかを表し、「オプション」はその動詞にとって必要とされる追加の情報です。 ドラキュラが新しいユーザーの場合、以下のようにコンピュータを設定します：

```bash
$ git config --global user.name "Vlad Dracula"
$ git config --global user.email "vlad@tran.sylvan.ia"
```

ここでは、ドラキュラの代わりに自分の名前とメールアドレスを使いましょう。 ここで入力した名前とメールアドレスは、これから行う Git での作業に関わってきます。というのも、これからのレッスンで[GitHub](https://github.com/)、[BitBucket](https://bitbucket.org/)、[GitLab](https://gitlab.com/)、またはその他のGit をホストするサーバーに変更箇所を「プシュ」した（送った）際に、これらの情報が使われるからです。

これらのレッスンでは、[GitHub](https://github.com/) に接続するので、GitHub アカウントと同じメールアドレスに設定してください。 プライバシーについて気になる方は、[GitHub のメールアドレスをプライベートにするための説明][git-privacy] を参照してください。

:::::::::::::::::::::::::::::::::::::::::  callout

## 電子メールの非公開

GitHub でプライベートのメールアドレスを使う場合は、同じメールアドレスを `user.email` の値に設定してください（例：`username@users.noreply.github.com`）。

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::  callout

## 改行コード

他のキーと同様に、キーボードで <kbd>Enter</kbd> または <kbd>↵</kbd> （またはMacでは <kbd>Return</kbd>）を押すと、コンピュータはそれを文字として入力します。
話が長くなるので詳しい説明は省きますが、行末に使われる文字はオペレーティングシステム（OS）よって違います。
（行末に使われる文字を「改行コード」と呼びます。）
Git は、改行コードを使ってファイルの違いを確かめるため、違うパソコンでファイルを編集した時に思わぬ問題が起こるかもしれません。
このレッスンの範囲外ですが、この問題については
[Pro Git book](https://www.git-scm.com/book/en/v2/Customizing-Git-Git-Configuration#_core_autocrlf) を読んでください。

Git がどのように改行コードを理解・変換するかは、 `git config` の `core.autocrlf` コマンドを使って変更できます。
以下の設定をおすすめします：

macOS および Linux:

```bash
$ git config --global core.autocrlf input
```

またはWindowsの場合:

```bash
$ git config --global core.autocrlf true
```

::::::::::::::::::::::::::::::::::::::::::::::::::

以下の表を参考に、ドラキュラはテキストエディタも設定しました：

| エディタ                           | 設定コマンド                                                                                                                           |
| :----------------------------- | :------------------------------------------------------------------------------------------------------------------------------- |
| Atom                           | `$ git config --global core.editor "atom --wait"`                                                                                |
| nano                           | `$ git config --global core.editor "nano -w"`                                                                                    |
| BBEdit（Mac、コマンドラインツール付き）       | `$ git config --global core.editor "bbedit -w"`                                                                                  |
| Sublime Text (Mac)             | `$ git config --global core.editor "/Applications/Sublime\ Text.app/Contents/SharedSupport/bin/subl -n -w"`                      |
| Sublime Text (Win、32ビットインストール) | `$ git config --global core.editor "'c:/program files (x86)/sublime text 3/sublime_text.exe' -w"`                                |
| Sublime Text (Win、64ビットインストール) | `$ git config --global core.editor "'c:/program files/sublime text 3/sublime_text.exe' -w"`                                      |
| メモ帳（Win）                       | `$ git config --global core.editor "c:/Windows/System32/notepad.exe"`                                                            |
| Notepad++ (Win、 32 ビットインストール)  | `$ git config --global core.editor "'c:/program files (x86)/Notepad++/notepad++.exe' -multiInst -notabbar -nosession -noPlugin"` |
| Notepad++ (Win、 64 ビットインストール)  | `$ git config --global core.editor "'c:/program files/Notepad++/notepad++.exe' -multiInst -notabbar -nosession -noPlugin"`       |
| Kate (Linux)                   | `$ git config --global core.editor "kate"`                                                                                       |
| Gedit (Linux)                  | `$ git config --global core.editor "gedit --wait --new-window"`                                                                  |
| Scratch (Linux)                | `$ git config --global core.editor "scratch-text-editor"`                                                                        |
| Emacs                          | `$ git config --global core.editor "emacs"`                                                                                      |
| Vim                            | `$ git config --global core.editor "vim"`                                                                                        |
| VS Code                        | `$ git config --global core.editor "code --wait"`                                                                                |

設定したテキストエディタもいつでも変更することができます。

:::::::::::::::::::::::::::::::::::::::::  callout

## Exiting Vim

Note that Vim is the default editor for many programs. If you haven't used Vim before and wish to exit a session without saving
your changes, press <kbd>Esc</kbd> then type `:q!` and hit <kbd>Enter</kbd> or <kbd>↵</kbd> or on Macs, <kbd>Return</kbd>.
If you want to save your changes and quit, press <kbd>Esc</kbd> then type `:wq` and hit <kbd>Enter</kbd> or <kbd>↵</kbd> or on Macs, <kbd>Return</kbd>.

::::::::::::::::::::::::::::::::::::::::::::::::::

Git (2.28+) allows configuration of the name of the branch created when you
initialize any new repository.  Dracula decides to use that feature to set it to `main` so
it matches the cloud service he will eventually use.

```bash
$ git config --global init.defaultBranch main
```

:::::::::::::::::::::::::::::::::::::::::  callout

## Default Git branch naming

Source file changes are associated with a "branch."
For new learners in this lesson, it's enough to know that branches exist, and this lesson uses one branch.\
By default, Git will create a branch called `master`
when you create a new repository with `git init` (as explained in the next Episode). This term evokes
the racist practice of human slavery and the
[software development community](https://github.com/github/renaming)  has moved to adopt
more inclusive language.

In 2020, most Git code hosting services transitioned to using `main` as the default
branch. As an example, any new repository that is opened in GitHub and GitLab default
to `main`.  However, Git has not yet made the same change.  As a result, local repositories
must be manually configured have the same main branch name as most cloud services.

For versions of Git prior to 2.28, the change can be made on an individual repository level.  The
command for this is in the next episode.  Note that if this value is unset in your local Git
configuration, the `init.defaultBranch` value defaults to `master`.

::::::::::::::::::::::::::::::::::::::::::::::::::

The five commands we just ran above only need to be run once: the flag `--global` tells Git
to use the settings for every project, in your user account, on this computer.

Let's review those settings and test our `core.editor` right away:

```bash
$ git config --global --edit
```

Let's close the file without making any additional changes.  Remember, since typos in the config file will cause
issues, it's safer to view the configuration with:

```bash
$ git config --list
```

And if necessary, change your configuration using the
same commands to choose another editor or update your email address.
This can be done as many times as you want.

:::::::::::::::::::::::::::::::::::::::::  callout

## Proxy

In some networks you need to use a
[proxy](https://en.wikipedia.org/wiki/Proxy_server). If this is the case, you
may also need to tell Git about the proxy:

```bash
$ git config --global http.proxy proxy-url
$ git config --global https.proxy proxy-url
```

To disable the proxy, use

```bash
$ git config --global --unset http.proxy
$ git config --global --unset https.proxy
```

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::  callout

## Git のヘルプとマニュアル

Always remember that if you forget the subcommands or options of a `git` command, you can access the
relevant list of options typing `git <command> -h` or access the corresponding Git manual by typing
`git <command> --help`, e.g.:

```bash
$ git config -h
$ git config --help
```

While viewing the manual, remember the `:` is a prompt waiting for commands and you can press <kbd>Q</kbd> to exit the manual.

More generally, you can get the list of available `git` commands and further resources of the Git manual typing:

```bash
$ git help
```

::::::::::::::::::::::::::::::::::::::::::::::::::

[git-privacy]: https://help.github.com/articles/keeping-your-email-address-private/

:::::::::::::::::::::::::::::::::::::::: keypoints

- Use `git config` with the `--global` option to configure a user name, email address, editor, and other preferences once per machine.

::::::::::::::::::::::::::::::::::::::::::::::::::
