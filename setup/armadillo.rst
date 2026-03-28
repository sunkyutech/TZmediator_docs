############
Armadillo-X2
############

ここでは，Armadillo-X2の実機を用いて実験を行う場合の方法について解説します．
詳細は `Armadillo-IoT ゲートウェイ G4/Armadillo-X2 セキュリティガイド <https://manual.atmark-techno.com/armadillo-x2/armadillo-base-os-security-guide_ja-1.8.1/>`_ の6章を参照してください．

Armadillo-X2のセットアップ
**********************************

Armadillo-X2を用いるための環境構築は，アットマークテクノ社が提供するVMを用いる方法とホストに構築する方法があります．
VMを用いることで，クロスコンパイルの環境構築を省略できますが，ホストで実行する方が高速かつシンプルです．

VMを用いる場合は，Armadillo-X2の `製品マニュアル 開発編 <https://manual.atmark-techno.com/armadillo-x2/armadillo-x2_product_manual_ja/ch03.html>`_ を参照ください．


Armadillo-X2への接続
**********************************

Armadillo-X2への接続には， ``minocom`` を使います．

``minocom`` がインストールされていない場合は，以下のコマンドでインストールしてください．

.. code-block:: bash

   sudo apt install minicom

.. hint::

    root権限なしで， ``minocom`` を使えるようにしておくと便利です．
    例えば，以下のコマンドで ``dialout`` グループにユーザを追加することができます．

    .. code-block:: bash

        sudo usermod -aG dialout $USER
        sudo shutdown -r now

``-D`` オプションでデバイスファイルを指定して ``minicom`` を起動します．

.. code-block:: bash

   minicom -D /dev/ttyUSB0

``minicom`` を終了するときは， ``Ctrl + a`` → ``z`` → ``x`` → ``Yes`` ，もしくは ``Ctrl + a`` → ``x`` → ``Yes`` で終了します．


リブータの使い方
***********************************

Armadillo-X2でプログラムを実行すると，度々再起動を必要とする事態に陥る可能性があります．
その場合，リモートで円滑に研究を進めるためにはリブータを活用することができます．

詳しくは，WATCH BOOT light RPC-M5CSの `取扱説明書 <https://www.rebooter.jp/detail/RPC-M5CS/RPC-M5CS.pdf>`_ を参照ください．

