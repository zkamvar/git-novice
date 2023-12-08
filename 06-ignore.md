---
title: ファイルを無視する
teaching: 5
exercises: 0
---

::::::::::::::::::::::::::::::::::::::: objectives

- Git で追跡したくないファイルを指定しましょう
- ファイルを無視する利点を理解しましょう

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Git で追跡したくないファイルを指定するにはどうすればよいですか？

::::::::::::::::::::::::::::::::::::::::::::::::::

Git に追跡して欲しくないファイル、例えばエディタが作成したバックアップファイルやデータ解析中に作られた中間ファイルなどは、どう対処すればいいのでしょう？
例として、いくつかファイルを作ってみましょう：

```bash
$ mkdir results
$ touch a.csv b.csv c.csv results/a.out results/b.out
```

そして Git が何と言うか見てみましょう：

```bash
$ git status
```

```output
On branch main
Untracked files:
  (use "git add <file>..." to include in what will be committed)

	a.csv
	b.csv
	c.csv
	results/

nothing added to commit but untracked files present (use "git add" to track)
```

これらのファイルをバージョンコントロールで保存するのはディスク容量の無駄になります。
さらに、これら全てが表示されると、本当に必要な変更点に集中できなくなってしまうかもしれないので、
Git にこれらのファイルを無視してもらいましょう。

これをするには、`.gitignore` というファイルをルートディレクトリに作ります：

```bash
$ nano .gitignore
$ cat .gitignore
```

```output
*.csv
results/
```

入力したパターンは、 Git に `.dat` で終わるファイル名と`results` ディレクトリ内にあるファイルを無視するように指示しています。
（Git がすでに追跡しているファイルは、引き続き追跡されます。）

このファイルを作った後`git status` の出力を見てみると、大分綺麗になっています：

```bash
$ git status
```

```output
On branch main
Untracked files:
  (use "git add <file>..." to include in what will be committed)

	.gitignore

nothing added to commit but untracked files present (use "git add" to track)
```

Git は新しく作られた `.gitignore` ファイルしか表示していません。
このファイルは追跡しなくても良いかと思うでしょうが、リポジトリを共有する際に、他の人達も私達が無視したものを同じように無視したいでしょう。
なので、`.gitignore` を追加してコミットしましょう：

```bash
$ git add .gitignore
$ git commit -m "Ignore data files and the results folder"
$ git status
```

```output
On branch main
nothing to commit, working tree clean
```

`.gitignore` を作った事によって、間違えて不要なファイルをリポジトリに追加する事を防ぐことができます：

```bash
$ git add a.csv
```

```output
The following paths are ignored by one of your .gitignore files:
a.csv
Use -f if you really want to add them.
```

この設定を強制的に無視してファイルを追加するには、`git add -f` を使います。 例えば、`git add -f a.csv` と入力します。
もちろん、無視されたファイルの状況はいつでも見ることができます：

```bash
$ git status --ignored
```

```output
On branch main
Ignored files:
 (use "git add -f <file>..." to include in what will be committed)

        a.csv
        b.csv
        c.csv
        results/

nothing to commit, working tree clean
```

:::::::::::::::::::::::::::::::::::::::  challenge

## 埋もれた（ネストされた）ファイルを無視する

以下のようなディレクトリ構造があるとします：

```bash
results/data
results/plots
```

`results/data` ではなく、`results/plots` のみを無視するにはどうすればいいのでしょう？

:::::::::::::::  solution

## Solution

If you only want to ignore the contents of
`results/plots`, you can change your `.gitignore` to ignore
only the `/plots/` subfolder by adding the following line to
your .gitignore:

```output
results/plots/
```

This line will ensure only the contents of `results/plots` is ignored, and
not the contents of `results/data`.

As with most programming issues, there
are a few alternative ways that one may ensure this ignore rule is followed.
The "Ignoring Nested Files: Variation" exercise has a slightly
different directory structure
that presents an alternative solution.
Further, the discussion page has more detail on ignore rules.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Including Specific Files

How would you ignore all `.csv` files in your root directory except for
`final.csv`?
Hint: Find out what `!` (the exclamation point operator) does

:::::::::::::::  solution

## Solution

You would add the following two lines to your .gitignore:

```output
*.csv           # ignore all data files
!final.csv      # except final.csv
```

The exclamation point operator will include a previously excluded entry.

Note also that because you've previously committed `.csv` files in this
lesson they will not be ignored with this new rule. Only future additions
of `.csv` files added to the root directory will be ignored.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Ignoring Nested Files: Variation

Given a directory structure that looks similar to the earlier Nested Files
exercise, but with a slightly different directory structure:

```bash
results/data
results/images
results/plots
results/analysis
```

How would you ignore all of the contents in the results folder, but not `results/data`?

Hint: think a bit about how you created an exception with the `!` operator
before.

:::::::::::::::  solution

## Solution

If you want to ignore the contents of
`results/` but not those of `results/data/`, you can change your `.gitignore` to ignore
the contents of results folder, but create an exception for the contents of the
`results/data` subfolder. Your .gitignore would look like this:

```output
results/*               # ignore everything in results folder
!results/data/          # do not ignore results/data/ contents
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Ignoring all data Files in a Directory

Assuming you have an empty .gitignore file, and given a directory structure that looks like:

```bash
results/data/position/gps/a.csv
results/data/position/gps/b.csv
results/data/position/gps/c.csv
results/data/position/gps/info.txt
results/plots
```

What's the shortest `.gitignore` rule you could write to ignore all `.csv`
files in `result/data/position/gps`? Do not ignore the `info.txt`.

:::::::::::::::  solution

## Solution

Appending `results/data/position/gps/*.csv` will match every file in `results/data/position/gps`
that ends with `.csv`.
The file `results/data/position/gps/info.txt` will not be ignored.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Ignoring all data Files in the repository

Let us assume you have many `.csv` files in different subdirectories of your repository.
For example, you might have:

```bash
results/a.csv
data/experiment_1/b.csv
data/experiment_2/c.csv
data/experiment_2/variation_1/d.csv
```

How do you ignore all the `.csv` files, without explicitly listing the names of the corresponding folders?

:::::::::::::::  solution

## Solution

In the `.gitignore` file, write:

```output
**/*.csv
```

This will ignore all the `.csv` files, regardless of their position in the directory tree.
You can still include some specific exception with the exclamation point operator.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## The Order of Rules

Given a `.gitignore` file with the following contents:

```bash
*.csv
!*.csv
```

What will be the result?

:::::::::::::::  solution

## Solution

The `!` modifier will negate an entry from a previously defined ignore pattern.
Because the `!*.csv` entry negates all of the previous `.csv` files in the `.gitignore`,
none of them will be ignored, and all `.csv` files will be tracked.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Log Files

You wrote a script that creates many intermediate log-files of the form `log_01`, `log_02`, `log_03`, etc.
You want to keep them but you do not want to track them through `git`.

1. Write **one** `.gitignore` entry that excludes files of the form `log_01`, `log_02`, etc.

2. Test your "ignore pattern" by creating some dummy files of the form `log_01`, etc.

3. You find that the file `log_01` is very important after all, add it to the tracked files without changing the `.gitignore` again.

4. Discuss with your neighbor what other types of files could reside in your directory that you do not want to track and thus would exclude via `.gitignore`.

:::::::::::::::  solution

## Solution

1. append either `log_*`  or  `log*`  as a new entry in your .gitignore

2. track `log_01` using   `git add -f log_01`

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- The `.gitignore` file tells Git what files to ignore.

::::::::::::::::::::::::::::::::::::::::::::::::::
