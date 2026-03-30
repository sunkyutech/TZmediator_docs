#################
WAMRの実装
#################

WAMR (Wasm Micro Runtime)は，WebAssemblyを実行するための軽量なランタイムです．
TZmediatorは，WAMRを利用して，Wasmアプリケーションをセキュアワールド内で実行します．

WAMRの実装はWaTZを参考にしています．
実装の詳細については，修論の第4章ならびにWaTZの `論文 <https://arxiv.org/pdf/2206.08722>`_ と `GitHub <https://github.com/JamesMenetrey/unine-watz>`_ を参照してください．

.. caution::

    WaTZは，実行するWasmアプリケーションのアテステーションに対応していますが，TZmediatorを用いて実行するアプリケーションのアテステーションが実行できることは確認できていません．
