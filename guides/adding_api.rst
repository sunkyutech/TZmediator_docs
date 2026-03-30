####################
APIの追加方法
####################

TZmediatorのAPIを追加するには，以下の手順で行います．

TZm-TAライブラリへの追加
***********************************

**step1: ヘッダファイルの作成**

``/libtzm-ta/include/`` ディレクトリに，追加するAPIのヘッダファイルを作成します．

.. hint::
    ヘッダファイルの命名規則は ``tz_`` + 従来のヘッダファイル名 + ``.h`` です．
    例えば，従来のヘッダファイル名が ``foo`` の場合，ヘッダファイルは ``tz_foo.h`` となります．

**step2: ソースファイルの作成**

``/libtzm-ta/src/`` ディレクトリに，追加するAPIのソースファイルを作成します．

.. hint::
    ソースファイルの命名規則は ``tz_`` + 従来のヘッダファイル名 + ``.c`` です．
    例えば，従来のヘッダファイル名が ``foo`` の場合，ソースファイルは ``tz_foo.c`` となります．

**step3: include_shimへのヘッダファイルの追加**

``/include_shim/`` ディレクトリに従来のヘッダファイルと同名のヘッダファイルを作成し，その中で作成したヘッダファイルをインクルードします．

.. code-block:: c

    #pragma once

    #include "tz_foo.h"

**step4: ライブラリのビルド**

:ref:`build_lib` と同様に，再度ライブラリをビルドします．

.. code-block:: bash

    cd linux-trustzone
    ./build_lib.sh


TZm-CAライブラリへの追加
***********************************

**step1: ヘッダファイルの作成**

``/libtzm-ca/include/`` ディレクトリに，追加するAPIのヘッダファイルを作成します．
この時，関数名は従来のAPIとは異なる名前にしてください．

**step2: ソースファイルの作成**

``/libtzm-ca/src/`` ディレクトリに，追加するAPIのソースファイルを作成します．

**step4: ライブラリのビルド**

:ref:`build_lib` と同様に，再度ライブラリをビルドします．


WASI・WAMRへの追加
************************

**step1: WASIへの追加**

``/wasi-sdk/src/wasi-libc`` ディレクトリ内から追加するAPIを探します．

追加したいAPIが見つかったら，そのAPIの実装を修正します．
以下のコードを追加する方法が最もシンプルです．

.. code-block:: c

    #include <wasi/api.h>

    #ifdef __use_tzmlib
	    return __wasi_foo(.., .., ..);
    #endif
    // 従来の実装
    ...

``/wasi-sdk/src/wasi-libc/libc-bottom-half/headers/public/wasi/api.h`` にAPIの宣言を追加します．

.. attention::

    WASIとネイティブの型サイズには十分に注意してください．
    例えば，WASIの ``size_t`` は32ビットであるため，ネイティブの ``size_t`` と同じサイズであるとは限りません．
    
    必要に応じて，WASIの型をネイティブの型に変換するコードを追加してください．
    また，``_Static_assert`` を使用して，型サイズが一致していることを確認することもできます．

**step2: WASIのビルド**

``/wasi-sdk/src/wasi-libc/Makefile`` を修正して，追加したAPIをビルドするようにします．

そして，再度WASIをビルドします．

.. code-block:: bash

    $ cd wasi-sdk/src/wasi-libc
    $ make EXTRA_CFLAGS="-D__use_tzmlib -D_WASI_EMULATED_SIGNAL -D_WASI_EMULATED_PROCESS_CLOCKS"

``/wasi-sdk/src/wasi-libc/sysroot/include/`` ディレクトリに，追加したAPIのヘッダファイルが配置され， ``/wasi-sdk/src/wasi-libc/sysroot/share/wasm32-wasi/undefined-symbols.txt`` に未定義のシンボルが記録されていることを確認します．

**step3: WAMRへの追加**

``/wasm-micro-runtime/core/iwasm/libraries/libc-wasi/`` に，step1で追加したAPIの実装を追加します．

ラッパー関数やヘッダファイルも必要に応じて追加してください．

``/wasm-micro-runtime/core/iwasm/libraries/libc-wasi/libc_wasi_wrapper.c`` において，以下のようにシンボルを定義しています．

.. code-block:: c

    #define REG_NATIVE_FUNC(func_name, signature)     \
        { #func_name, wasi_##func_name, signature, NULL }

    static NativeSymbol native_symbols_libc_wasi[] = {
        REG_NATIVE_FUNC(foo, "(ii*)i"),

``wasi_foo`` 関数からTZm-TAライブラリのAPIを呼び出すようにします．

**step4: WAMRのビルド**

再度WAMRをビルドします．

.. code-block:: bash

    $ ./build.sh

