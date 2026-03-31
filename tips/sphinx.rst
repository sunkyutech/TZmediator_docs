######################################
Sphinxを用いたドキュメントの作成
######################################

Sphinxを利用してプロジェクト全体のドキュメントを作成することができます．

環境構築と初期設定
===============================

.. hint::

   Sphinxのインストール方法からrst形式の書き方まで， `Sphinxの使い方 <https://zenn.dev/y_mrok/books/sphinx-no-tsukaikata>`_ の記事が非常に参考になります．
   こちらも併せてご覧ください．

ここでは，簡単にSphinxの使い方を説明します．

まずは，Pythonがインストールされていることを確認してください．

.. code-block:: bash

   $ python --version
   Python 3.10.4


SphinxはPython標準のドキュメント生成ツールであり， ``sphinx-quickstart`` コマンドによって基本的なディレクトリ構造を即座に生成できます．

.. code-block:: bash

   # Sphinxのインストール
   pip install sphinx sphinx_rtd_theme

   # プロジェクトの初期化（対話形式でプロジェクト名などを入力）
   sphinx-quickstart

この操作により，設定ファイル (``conf.py``) とインデックスファイル (``index.rst``) が作成されます．

ドキュメントの編集・プレビューは，VSCodeのSphinx拡張機能が便利です．
(`Extension Pack for reStructuredText <https://marketplace.visualstudio.com/items?itemName=lextudio.restructuredtext-pack>`_)

.. note::

   ライブプレビューを利用するには，パスを正しく設定する必要があります．

   .. code-block:: bash

      {
         "esbonio.sphinx.confDir": "{workspaceFolder}", // conf.pyが置かれているディレクトリを指定
         "esbonio.server.enabled": true, // デフォルト true になっているはず
         "esbonio.sphinx.buildDir": "{workspaceFolder}/_build", // ビルドで生成されるHTMLファイルなどの出力先
         "restructuredtext.linter.doc8.extraArgs": ["--max-line-length", 200] // linterの設定（任意）
      }
   
   また，reStructureText用の言語サーバ ``esbonio`` をインストールする必要があります．

   .. code-block:: bash

      pip install esbonio


ビルドと共有
============================

ドキュメントの生成は， ``make`` コマンドを実行します．

.. code-block:: bash

   # HTML形式でドキュメントをビルド
   make html

生成された ``_build/html/index.html`` をブラウザで開くことで，ローカル環境で完成形を確認できます．

.. hint::

   公式ドキュメントなどでよく見るテーマは， ``sphinx_rtd_theme`` です．
   以下のコマンドでインストールできます．

   .. code-block:: bash

      pip install sphinx_rtd_theme
   
   ``conf.py`` を開いて， ``html_theme`` を修正します．

   .. code-block:: python

      html_theme = "sphinx_rtd_theme"

   再度， ``make html`` を実行してビルドし直すと，テーマが変更されていることが確認できます．

Sphinxで作成したドキュメントをGitHubにアップロードすると `GitHub Pages <https://docs.github.com/ja/pages/getting-started-with-github-pages/what-is-github-pages>`_ や `Read the Docs <https://about.readthedocs.com/?ref=app.readthedocs.org>`_ で一般公開することもできます．

Webサーバをお持ちであれば，Sphinxで作成したHTMLファイルを所定のディレクトリにアップロードすることで表示することも可能です．

さらに，PDF形式にも出力できます．
