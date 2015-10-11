# pandas sprint

- 目的

  - とりあえず触ってみたい
    - [10 minutes to pandas](http://pandas.pydata.org/pandas-docs/stable/10min.html)
  - コードリーディングしたい
  - プルリクエスト (PR) を送りたい

## 全体の流れ (PR)

1. 準備
2. issue を調べる
3. コードの修正/テストの追加
4. プルリクエスとの記載
5. マージを待つ

PRマージされると[リリースノート](http://pandas.pydata.org/pandas-docs/stable/release.html)/通知に名前が載る (匿名可)

## 準備

- Git をインストールする
- GitHubアカウントを作成する
- [pandas](https://github.com/pydata/pandas) のリポジトリをフォークする
- Travis CI の設定をする (GitHub/Travis双方)
- ローカルにクローンする (``git@github.com:xxx/pandas.git``)
- (必要なら) 仮想環境作る
- ``setup.py develop`` でインストールする 
  - 仮想環境切り替えでCythonのリコンパイルをする場合は ``setup.py clean`` する

## issue を調べる

- openのもの
- issue のラベル (付与されていないものもあるため参考程度)
  - 機能別
  - (想定)難易度別 ("Difficulty ...")
    - [Novice](https://github.com/pydata/pandas/labels/Difficulty%20Novice)
    - [Intermediate](https://github.com/pydata/pandas/labels/Difficulty%20Intermediate)
    - [Advanced](https://github.com/pydata/pandas/labels/Difficulty%20Advanced)
  - (想定)工数のフラグ ("Effort ...") 
    - [Low](https://github.com/pydata/pandas/labels/Effort%20Low)
    - [Medium](https://github.com/pydata/pandas/labels/Effort%20Medium)
    - [High](https://github.com/pydata/pandas/labels/Effort%20High)
  - 横串管理されているもの (以下のissue群)からリンクされているもの
    - [Master Tracker](https://github.com/pydata/pandas/labels/master%20tracker)
      - [Index/Series Names...](https://github.com/pydata/pandas/issues/9862)は比較的簡単
- 機能追加 [Enhancement](https://github.com/pydata/pandas/labels/enhancement) は (バグ修正と比べ) PR後の議論が長くなる場合が

- 難易度 (個人の感想です)

  - DataFrame/Series のメソッドを直す
    - farme.py / series.py に実装があるものは(比較的)簡単
    - generic の中は少し手間
  - エラーメッセージを直す ("Error Reporting")
  - plotting / output-formatting は他機能に影響することが(ほぼ)ないので修正は楽 / テスト準備が手間な場合も
  
- 作業中のissueは重複しないようホワイトボード(あれば)に書く
  
## コードの修正/テストの追加

1. コード本体の修正
2. テストの追加 (PRする場合 MUST)
3. リリースノートの追加 (PRする場合 MUST)

- 共通で使える関数/メソッドがあるのはこのあたり

  - pandas
    - core
      - base: Index/Series で共通のメソッドがある
      - common: 型のチェックなどよく使われる関数がある
      - generic: Series/DataFrame で共通のメソッドがある
    - tseries 
      - base: DatetimeIndex/PeriodIndex/TimedeltaIndex で共通のメソッドがある
    - compat: py2/py3 で差異のある関数/変数の定義がある

- テスト用の関数はこちら

  - util.testing
    - ``assert_index_equal``: ``pd.Index`` の比較
    - ``assert_series_equal``: ``pd.Series`` の比較
    - ``assert_frame_equal``: ``pd.DataFrame`` の比較
    - ``assertRaises``: 異常ケースで期待するエラー発生するかチェック
    - ``assertRaisesRegexp``: 異常ケースで期待するエラー/エラーメッセージが発生するかチェック
    - ``assert_produces_warning``: 期待する警告が発生するかチェック

- テストには issue 番号をコメントで書いたほうがよい (``# GH 10000`` など)

- リリースノート
  - doc/source/whatsnew/v0.17.1.txt
  - バグ修正の場合、何の機能を使ったときにどういった問題が起きていたかを書く
  - ビルド確認は doc/make.py (環境によっては sudo 必要)
  - リリースノートに一行追加する程度であれば 目視確認でもOK (リリース前にまとめて直すので)

English
=======

....
