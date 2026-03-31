##############
ビルド手順
##############

TZmediatorのビルドは，以下の手順で行います．

step 1 - ソースコードの取得
*****************************

まず，TZmediatorおよび関連リポジトリを取得します．

必要に応じて，サブモジュールを取得します．

.. code-block:: bash

    $ git submodule update --init --recursive


step 2 - ビルド環境の構築
******************************

TZmediatorのビルドには，以下のツールチェーンおよび依存パッケージが必要です．

- クロスコンパイラ（aarch64-linux-gnu-gcc など）
- OP-TEEビルド環境
- make, cmake, ninja などのビルドツール
- その他，必要なライブラリやツール (詳細はOP-TEEドキュメントを参照)

例：

.. code-block:: bash

    $ sudo apt update
    $ sudo apt install build-essential git cmake python3

クロスコンパイラのパスを環境変数に設定します．

.. code-block:: bash

    export CROSS_COMPILE=<ツールチェーンのパス>/aarch64-linux-gnu-

また，OP-TEE関連の環境変数を設定します．

.. code-block:: bash

    export OPTEE_OS_DIR=<optee_osのパス>
    export OPTEE_CLIENT_EXPORT=<optee_clientのパス>
    export TA_DEV_KIT_DIR=<TA dev kitのパス>


step 3 - OP-TEE OSのビルド
*********************************

OP-TEE OSをビルドします．

.. code-block:: bash

    $ cd <opteeビルドディレクトリ>
    $ make -j$(nproc) run

.. attention::

    クロスコンパイル環境でビルドする場合は，対象アーキテクチャに注意してください．


.. _build_lib:
step 4 - ライブラリのビルド
**********************************

OP-TEE Clientライブラリをビルドします．

.. code-block:: bash

    $ cd <TEE Clientライブラリのディレクトリ>
    $ make -C imx-optee-client \
        DESTDIR="${PWD}/out" \
        CROSS_COMPILE="aarch64-linux-gnu-" \
        TA_DEV_KIT_DIR="${PWD}/imx-boot-[VERSION]/imx-optee-os/out/export-ta_arm64"

TZmライブラリをビルドします．
``build_lib.sh`` のスクリプトを使用してビルドすることができます．

.. code-block:: bash

    cd linux-trustzone
    ./build_lib.sh

.. note::

    TZmライブラリのビルドには，TEE Clientライブラリ， ``TA_DEV_KIT_DIR`` ， ``TA_SIGN_KEY`` が必要です．
    ``build_lib.sh`` の中身を適宜編集して，環境に合わせて設定してください．


step 5 - アプリケーションのビルド
*************************************

CA側で動作するアプリケーションをビルドします．

TZmediatorを使用するには， ``teecライブラリ (libteec.a)`` と　``TZm-CAライブラリ (libtzm-ca.a)`` をリンクする必要があります．

TA側で動作するアプリケーションをビルドします．

CAに対応したTAとしてビルドするには， ``teecライブラリ (libteec.a)`` と　``TZm-TAライブラリ (libtzm-ta.a)`` をリンクする必要があります．

.. hint::

    TAのビルドには， ``ta-cc`` を使用することができます．
    ta-ccの詳細については，:ref:`ta-cc_usage` を参照してください．
