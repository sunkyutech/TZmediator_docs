.. _jupyter:
####################################################
Jupyter Notebookを用いた実験データの分析と可視化
####################################################

ここでは，Jupyter Notebookを活用して実験ログから定量的な知見を導き，図や表として出力するまでの一連のワークフローを解説します．

環境構築
==============

Jupyter Notebookの環境は，VSCodeの拡張機能が便利です．

分析
==============

まず，冒頭で関連ライブラリをインポートします．
また，プロジェクト全体で用いる定数を集約しておきます．

.. code-block:: python

   import pandas as pd
   import matplotlib.pyplot as plt
   import matplotlib as mpl
   from pathlib import Path

   # グラフのスタイル一括設定：論文や報告書向けのフォント設定
   mpl.rcParams["font.family"] = ["DejaVu Sans", "IPAexGothic"]
   mpl.rcParams['pdf.fonttype'] = 42 # PDF出力時のフォント埋め込み

   BASE_DIR = Path("ipc-bench")
   # 分析対象を辞書形式で定義し，コード内での可読性と保守性を両立させる
   TECH_LABEL = {"fifo": "名前付きパイプ", "tcp": "TCPソケット"}

.. note::

    生成したグラフをPDFに出力して論文などに掲載するする場合には，グラフを埋め込んでおく必要があります．

情報は抽出しやすいデータを出力・保存しておくことが望ましいです．

- CSVファイル
- LOGファイル

非構造データを用いる場合は，情報を抽出 (パース)します．
正規表現 (re) を用いて必要な数値を抽出します．

.. code-block:: python

   import re

   # 正規表現パターンの定義：Average durationなどの特定の行を狙い撃つ
   AVG_RE = re.compile(r"^\s*Average duration:\s*([0-9]*\.?[0-9]+)\s*([a-zA-Z]+)\s*$", re.MULTILINE)

   def parse_log(path: Path):
       text = path.read_text(errors="replace")
       avg_m = AVG_RE.search(text)
       if avg_m:
           # 単位変換ロジックをカプセル化し，分析データの単位を統一（例：すべてusに変換）
           return float(avg_m.group(1)) 
       return None

Pandasを活用してデータを構造化します．
個別のファイルから抽出したデータをリストに格納し，最終的にPandasのDataFrameへ変換します．
これにより，大量の実験結果をテーブル形式で俯瞰でき，フィルタリングや並べ替えが容易になります．

.. code-block:: python

   rows = []
   for tech in technologies:
       # ファイルパスの動的生成
       log_path = BASE_DIR / tech / "data.log"
       val = parse_log(log_path)
       rows.append({"technology": tech, "avg_us": val})

   df = pd.DataFrame(rows)
   # データの欠損や異常値を即座にプレビュー確認
   display(df.head())

Matplotlibを用いて，分析結果をグラフ化します．
Jupyter Notebook上では図をインラインで確認できるため，エラーバーの付与や，データが存在しない箇所への「N/A」注釈など，細かい表現の作り込みを対話的に行います．
PDF形式に出力して，そのまま論文に掲載することもできます．
また，Excel形式に出力して，プレゼンテーション (PowerPoint) に用いるグラフを作成することもできます．

.. code-block:: python

   fig, ax = plt.subplots(figsize=(7, 3.0))
   
   # 複数条件の比較を行うグループ化棒グラフの描画
   ax.bar(x, y, yerr=std_dev, capsize=8, label="計測値")

   # N/A（欠損値）の明示：データがないことを「見える化」する
   for i, val in enumerate(y):
       if np.isnan(val):
           ax.annotate("N/A", xy=(i, 0), ha="center", va="bottom", rotation=90)

   ax.set_ylabel("レイテンシ (μs)")
   plt.tight_layout()
   plt.savefig("output.pdf") # ベクター形式での保存

定量的な考察についても，Pythonプログラムから計算を自動化するとよいです．

.. code-block:: python

   # データの再整形（ピボット）による条件間比較
   pivot = df.pivot(index="technology", columns="type", values="avg_us")
   # 改善率の算出：人手による計算ミスを排除
   improvement_ratio = (pivot["legacy"] - pivot["optimized"]) / pivot["legacy"] * 100.0
   print(f"改善率の平均: {improvement_ratio.mean():.2f}%")
