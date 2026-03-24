#####################
ベンチマークの測定
#####################

TZmediatorの性能を測定するためのベンチマークの測定方法について説明します．
マイクロベンチマークとして，IPC-BenchとLMbenchを使用します．
アプリケーションベンチマークとして，DarkneTZを使用します．

IPC-Bench
*********

IPC-Benchは，プロセス間通信の性能を測定するためのベンチマークツールです．
詳細は，IPC-Benchの `GitHubリポジトリ <https://github.com/goldsborough/ipc-bench>`_ を参照してください．
測定できる通信方式には，以下のようなものがあります．

- 名前なし/名前付きパイプ
- UNIXドメインソケット
- TCPソケット
- メッセージキュー
- ZeroMQ (TCP)
- 共有メモリ
- メモリマップドファイル

.. caution::
    IPC-Benchは，UDPソケットやセマフォの測定には対応していません．
    また， ``pthread`` を用いた通信を行うためのコードが存在しますが，適切な実装ではありません．

実行すると，以下のような出力が得られます．

.. code-block:: bash

    ============ RESULTS ================
    Message size:       4096
    Message count:      1000
    Total duration:     1.945      	ms
    Average duration:   1.418      	us
    Minimum duration:   0.000      	us
    Maximum duration:   25.000     	us
    Standard deviation: 1.282      	us
    Message rate:       514138     	msg/s
    =====================================

.. note::
    メッセージレートは，メッセージサイズと合計通信時間から計算されます．
    そのため，平均通信時間とメッセージレートは，必ずしも単純な逆数の関係にはなりません．
    また，スループットとも異なる指標であることに注意してください．

IPC-Benchをビルドするには，以下のコマンドを実行します．

.. code-block:: bash

IPC-Benchを実行するには，以下のコマンドを実行します．

.. code-block:: bash



LMbench
*******

LMbenchは，ネットワークやメモリ，ファイルシステムなどの様々なパフォーマンスを測定するためのベンチマークツールです．
詳細は，LMbenchの `公式サイト <https://lmbench.sourceforge.net/>`_ や `GitHubリポジトリ <https://github.com/intel/lmbench>`_ を参照してください．

.. note::
    LMbenchには，プロセス間通信の性能を測定するためのベンチマークが含まれています．
    ただし，これらのベンチマークは ``fork`` を用いるため，TZmediatorの性能を測定するには適していません．

LMbenchをビルドするには，以下のコマンドを実行します．

.. code-block:: bash

    make

LMbenchを実行するには，以下のコマンドを実行します．

.. code-block:: bash

    ./lmbench


DarkneTZ
********

DarkneTZは，C言語でDNN推論を行うためのDarknetをOP-TEE上で動作させるための研究です．
詳細は，DarkneTZの `論文 <https://dl.acm.org/doi/10.1145/3386901.3388946>`_ や `GitHubリポジトリ <https://github.com/mofanv/darknetz>`_ を参照してください．

DarkneTZは，OP-TEEを用いてDNNの学習と推論を行うことができます．


実行すると，以下のような出力が得られます．

.. code-block:: bash

    darknetp classifier predict -pp_start 4 -pp_end 10 cfg/mnist.dataset cfg/mnist_lenet.cfg models/mnist/mnist_lenet.weights  data/mnist/images/t_00007_c3.png

DarkneTZをビルドするには，以下のコマンドを実行します．

.. code-block:: bash

    make

DarkneTZを実行するには，以下のコマンドを実行します．

.. code-block:: bash

    ./darknet
