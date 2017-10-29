# 工学部専門科目「プログラミング言語」(2017年度)

## 課題1 (締切 11/13 (月) 10:30)

__計算木__ とは以下のような2分木の一種である．

* 葉 (`leaf`) は計算木である．ただし，葉には正整数が格納されている．
* ふたつの計算木 t1 と t2 に対し，枝 (`branch(t1, t2)`) は計算木である．ただし，枝にはタイプSの枝とタイプMの枝の二種類がある．

この時，計算木の価値を以下のように定義する．

* 葉の価値は，格納された整数値そのものである．
* 枝の価値は，タイプSの枝の場合は部分木の価値の和，タイプMの枝の場合は部分木の価値の積である．

### 課題1-1-1

Java で計算木のデータ構造をオブジェクトを使って定義し，価値を計算するためのメソッド `int value()` を定義せよ．

### 課題1-1-2

計算木にタイプXの枝を追加する．タイプXの枝の価値は，(t1の価値)の(t2の価値)乗となる．タイプXの枝を表すオブジェクトのクラス名は `BranchX` として，メソッド `int value()` を定義せよ．

注意: 課題1-1-3〜1-1-7については，タイプXの枝は無視しても構わない．ただし，メソッドの定義がないとコンパイルできないので，適当な値を返すダミー定義を与えればよい．(もちろんタイプXを考慮してもらっても構わない．その場合は課題の説明にタイプXも考慮したことを明記せよ．)

### 課題1-1-3

課題1-1-1のプログラムを元にして，計算木の価値を表す計算式(の文字列)に変換するメソッド `String toString()` を定義せよ．例えば，1を格納した葉と2を格納した葉を部分木として持つタイプSの枝の変換結果は `"(1+2)"`となる．タイプMの枝については `*` を，タイプXの枝については(必須ではないが) `^` を使うこと．簡単のために枝毎に括弧をつけよ．

注意: 単に木の価値を計算してからその結果(この例であれば `"3"`) を答えとするのは認めない．つまり，葉に格納された数値は全て文字列に含まれるようにせよ．また，枝毎に括弧をつけるので，一番外側の括弧がない`"1+2"` のような文字列は正解ではないことにも注意せよ．

### 課題1-1-4(オプション)

課題1-1-3のプログラムを元にして，括弧を適宜省いた文字列に変換するようなメソッド `String toStringFewerParens()` を定義せよ．この時(いつもの算数の通り) `*` は `+` より結合が強く，どちらも左結合であると考える．すなわち

* `"((2*4)+3)"` → `"2*4+3"` はOK
* `"((2+4)*3)"` → `"2+4*3"` はダメ
* `"((2+4)*3)"` → `"(2+4)*3"` はOK
* `"((1+2)+3)"` → `"1+2+3"` はOK
* `"(1+(2+3))"` → `"1+2+3"` はダメ
* `"(1+(2+3))"` → `"1+(2+3)"` はOK
* `"((1*2)*3)"` → `"1*2*3"` はOK
* `"(1*(2*3))"` → `"1*2*3"` はダメ
* `"(1*(2*3))"` → `"1*(2*3)"` はOK

「○○演算子が左結合である」とは「同じ演算子が括弧がなく並んだ時には左側に括弧がつくように解釈する」という意味である．足し算やかけ算については結合則が成立しないので，どちらに結合しても式の値は変わらないのであまり結合に拘ることに意味はないが，例えば引き算演算子は左結合であることが重要である．

タイプXの枝について(オプション): `^` は `*` よりも結合が強く，右結合である．

* `"((2^4)*3)"` → `"2^4*3"` はOK
* `"((1^2)^3)"` → `"1^2^3"` はダメ
* `"((1^2)^3)"` → `"(1^2)^3"` はOK
* `"(1^(2^3))"` → `"1^2^3"` はOK

### 課題1-1-5(オプション)

課題1-1-1のプログラムを元にして，計算木中の葉の数を数えるメソッド `int countLeaf()` と，計算木の高さを数えるメソッド `int height()` を定義せよ．計算木の高さは，根から各葉までの経路を考えた時に通過する枝の数の最大値として定義される．

### 課題1-1-6(オプション)

課題1-1-1のプログラムを元にして，以下のような「木の簡約操作」を行うようなメソッド `Tree reduce()` を定義せよ．

> 簡約操作: ふたつの葉を部分木として持つ枝一箇所を選んで，その部分木を，その部分木の価値を格納した葉で置換する．木に該当箇所がひとつもない場合には，入力された木がそのまま出力となる．

例えば，
```
    *
   / \
  +   +
 / \ / \
1  2 3  4
```
は，
```
    *
   / \
  3   +
     / \
     3  4
```
または，
```
    *
   / \
  +   7
 / \
1  2
```
のどちらかに簡約される．

枝の選び方についてどのように定めたかレポートに明記せよ．また，`reduce` 前の計算木が破壊されないよう，永続的なデータ構造になるよう定義せよ．

### 課題1-1-7(オプション)

課題1-1-1のプログラムを元にして，計算木中の `n` を格納した葉を全て計算木 `t` で置き換えたような計算木を生成するメソッド `Tree subst(int n, Tree t)` を定義せよ．

例えば，
```
    *
   / \
  +   +
 / \ / \
1  2 3  4
```
の `3` を，
```
  *
 / \
6   7
```
で置き換えると
```
    *
   / \
  +   +
 / \ / \
1  2 *  4
    / \
   6   7
```
が得られる．

課題1-6-1と同様，永続的なデータ構造になるよう定義せよ．

### 課題1-2-1

OCaml で計算木のデータ構造をヴァリアントを使って定義し，価値を計算するための関数 `value_of_tree t` を定義せよ．

### 課題1-2-2

課題1-2-1のプログラムを元にして，計算木の定義に課題1-2にあるタイプXの枝を追加し，拡張された計算木の価値を計算するための関数 `value_of_tree2 t` の定義をせよ．

注意: 課題1-2-3〜1-2-7の課題については，タイプXの枝は無視しても構わない．パターンマッチの網羅性についての警告が出てくるが無視してよい．(もちろんタイプXを考慮してもらっても構わない．その場合は課題の説明にタイプXも考慮したことを明記せよ．)

### 課題1-2-3

課題1-2-1のプログラムを元にして，計算木の価値を表す計算式(の文字列)に変換する関数 `string_of_tree t` を定義せよ．OCaml での文字列の連結に中置演算子 `^` を使う．

```{.ocaml}
# let s1 = "This is ";;
val s1 : string = "This is "
# s1 ^ "a pen.";;
- : string = "This is a pen."
```

その他の注意は課題1-1-3と同じである．

### 課題1-2-4(オプション)

課題1-2-3のプログラムを元にして，括弧を適宜省いた文字列に変換するような関数 `string_of_tree_fewer_parens t` を定義せよ．その他の注意は課題1-1-4と同じである．

### 課題1-2-5(オプション)

課題1-2-1のプログラムを元にして，計算木中の葉の数を数える関数 `count_leaf t` と，計算木の高さを数える関数 `height t` を定義せよ．計算木の高さは，根から各葉までの経路を考えた時に通過する枝の数の最大値として定義される．

### 課題1-2-6(オプション)

課題1-2-1のプログラムを元にして，課題1-1-6にある「木の簡約操作」を行うような関数 `reduce t` を定義せよ．

### 課題1-2-7(オプション)

課題1-2-1のプログラムを元にして，計算木 `t` 中の `n` を格納した葉を全て計算木 `t'` で置き換えたような計算木を生成するメソッド `subst(t, n, t')` を定義せよ．

## プログラム作成上の注意

* このリポジトリにはプログラムの雛形が含まれている．この雛形を用いて課題を行うこと．特にメソッドのシグネチャは変えないこと．
* このリポジトリには簡単なテストも含まれている．単にメソッドや関数の定義を与えるだけでなく，テストを用いてそれがうまく動くことを確認せよ．自分でテストを拡張して幅広い具体例に対してテストせよ．テストの追加は `java/TestCase.java` `ocaml/testcase.ml` を見れば想像つくかと思うが，
    * Java の場合は14行目と15行目の間に，計算木オブジェクト(を表す式)を追加する．区切りはコロンを使う．
    * OCaml の場合は13行目と14行目の間に，`tree` 型の式を追加する．区切りはセミコロンを使う．
また，課題1-1-7, 1-2-7 については，テストケース(2n-1)番目の木の中の 3 に対し，2n番目の木を代入するようなテストが行われる．
* コンパイルができないプログラムを提出した場合には採点の対象外となる．
* Java のパッケージ機能は(コンパイルする環境に依存しがちなので)使わないこと．

### Java プログラムのテスト実行方法

`TestX.java` がテストなので，全てのファイルをコンパイルしてから，`TestX` (の `main` メソッド) を実行する．

### 複数のOCamlファイルからなるプログラムのビルド方法

このリポジトリの `ocaml` ディレクトリには，OCamlの課題のテストの実行を補助するための Makefile が含まれている．端末上で `ocaml` ディレクトリの中まで行き， `make test1.out` と実行すると，1行目に

```
ocamlopt tree.ml testcase.ml test1.ml -o test1.out
```

と表示される．

* `ocamlopt` はOCamlソースファイルを実行可能ファイルへ変換するコマンドである．
* `ocamlopt` コマンドの後には `tree.ml testcase.ml test1.ml` のように作りたいプログラムのもとになるソースファイルを列挙する．
    * このとき，依存されるソースファイルは依存するソースファイルよりも前に並べる必要がある．
    * 今回の場合， `testcase.ml` は `tree.ml` に依存し， `test1.ml` は `tree.ml` と `testcase.ml` の両方に依存するので， `tree.ml testcase.ml tree.ml`の順番に並べなければならない．
* `-o test1.out` は出力する実行可能ファイルの名前を `test1.out` に指定する．このオプションを省略すると出力ファイルは `a.out` となる．

生成された実行可能ファイルを実行するとテスト結果が表示される．

## 提出要領

1. https://github.com/ProgrammingLanguagesAtKUEng/kadai1 からファイルをダウンロードする．(git 使いはもちろん clone してもよい．)
2. Java プログラムおよびそのテストは `java` フォルダに入れること．OCaml プログラムおよびそのテストは `ocaml` フォルダに入れること．
3. プログラムの説明を `report.md` (Markdown もしくは plain text 形式)に書け．課題毎に説明すること．内容だけでなく読みやすさも採点の対象となる．これは，この `README.md` と同じフォルダに置くこと．(上記のURLからダウンロードすると雛形が含まれている．)
4. プログラムの説明を入れたフォルダを圧縮して zip ファイルを作り，PandA で提出すること．
