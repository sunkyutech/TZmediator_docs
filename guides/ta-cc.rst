.. _ta-cc_usage:
###################
ta-ccの使い方
###################

TAのビルドには， ``ta-cc`` を使用することができます．

``ta-cc`` は，TAとして動作するアプリケーションをビルドするためのGCCライクなスクリプトです．
スクリプトの中身の詳細については，修論の4章を参照してください．

まず，TAのビルドに必要な環境変数を設定します．

.. code-block:: bash

    export OPTEE_OS_DIR=<optee_osのパス>
    export OPTEE_CLIENT_EXPORT=<optee_clientのパス>
    export TA_DEV_KIT_DIR=<TA dev kitのパス>

次に，TAのソースコードがあるディレクトリに移動し，以下のコマンドを実行します．
この時，ソースファイルは複数指定することができます．

.. code-block:: bash

    ta-cc <src>.c -o <UUID>.ta

インクルードファイルが必要な場合は， ``-- -I`` オプションを使用してインクルードディレクトリを指定します．

.. code-block:: bash

    ta-cc <src>.c -o <UUID>.ta -- -I <インクルードディレクトリ>
