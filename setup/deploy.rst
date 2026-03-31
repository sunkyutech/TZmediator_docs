#############
デプロイ
#############

(TZmediatorの使用有無に関わらず) ビルドしたTAは， ``/usr/lib/optee_armtz/`` に配置する必要があります．

QEMUの場合
**************************

``make run`` コマンドを実行すると，ビルドしたTAがQEMU上の ``/usr/lib/optee_armtz/`` に自動的に配置されます．

また，ビルドしたTAをQEMU上に手動で配置することもできます．


Armadillo-X2の場合
**************************

TAを適切な場所に配置する必要があります．

Armadillo-X2の公式ドキュメントでは，tarballで固めて転送し，ターゲット上のコンテナで展開する方法が紹介されています．

以下のコマンドでコンテナを起動します．

.. code-block:: bash

    [armadillo ~]# podman run -it --name=dev_optee --device=/dev/tee0 \
        --device=/dev/teepriv0 -v "$(pwd)":/mnt docker.io/debian /bin/bash

.. note::

    ``--device=/dev/tee0`` と ``--device=/dev/teepriv0`` は，TAがTEEデバイスにアクセスできるようにするためのオプションです．
    これらのオプションを使用することで，コンテナ内からTAがTEEデバイスにアクセスできるようになります．

コンテナ内で，tarballを展開してTAを配置します．

.. code-block:: bash

    [container ~]# tar xavf /path/optee.tar.gz -C /
    ./
    ./lib/
    ./lib/optee_armtz/
    ./lib/optee_armtz/b3091a65-9751-4784-abf7-0298a7cc35ba.ta
    ./lib/optee_armtz/731e279e-aafb-4575-a771-38caa6f0cca6.ta
    ./lib/optee_armtz/873bcd08-c2c3-11e6-a937-d0bf9c45c61c.ta
    ./lib/optee_armtz/5b9e0e40-2636-11e1-ad9e-0002a5d5c51b.ta
    ./lib/optee_armtz/690d2100-dbe5-11e6-bf26-cec0c932ce01.ta
    ./lib/optee_armtz/528938ce-fc59-11e8-8eb2-f2801f1b9fd1.ta
    ./lib/optee_armtz/f157cda0-550c-11e5-a6fa-0002a5d5c51b.ta
    ./lib/optee_armtz/d17f73a0-36ef-11e1-984a-0002a5d5c51b.ta
    ./lib/optee_armtz/8aaaf200-2450-11e4-abe2-0002a5d5c51b.ta
    ./lib/optee_armtz/c3f6e2c0-3548-11e1-b86c-0800200c9a66.ta
    ./lib/optee_armtz/f04a0fe7-1f5d-4b9b-abf7-619b85b4ce8c.ta
    ./lib/optee_armtz/b6c53aba-9669-4668-a7f2-205629d00f86.ta
    ./lib/optee_armtz/a734eed9-d6a1-4244-aa50-7c99719e7b7b.ta
    ./lib/optee_armtz/380231ac-fb99-47ad-a689-9e017eb6e78a.ta
    ./lib/optee_armtz/a4c04d50-f180-11e8-8eb2-f2801f1b9fd1.ta
    ./lib/optee_armtz/5dbac793-f574-4871-8ad3-04331ec17f24.ta
    ./lib/optee_armtz/023f8f1a-292a-432b-8fc4-de8471358067.ta
    ./lib/optee_armtz/5ce0c432-0ab0-40e5-a056-782ca0e6aba2.ta
    ./lib/optee_armtz/cb3e5ba0-adf1-11e0-998b-0002a5d5c51b.ta
    ./lib/optee_armtz/fd02c9da-306c-48c7-a49c-bbd827ae86ee.ta
    ./lib/optee_armtz/484d4143-2d53-4841-3120-4a6f636b6542.ta
    ./lib/optee_armtz/f4e750bb-1437-4fbf-8785-8d3580c34994.ta
    ./lib/optee_armtz/e6a33ed4-562b-463a-bb7e-ff5e15a493c8.ta
    ./lib/optee_armtz/e13010e0-2ae1-11e5-896a-0002a5d5c51b.ta
    ./lib/optee_armtz/614789f2-39c0-4ebf-b235-92b32ac107ed.ta
    ./lib/optee_armtz/25497083-a58a-4fc5-8a72-1ad7b69b8562.ta
    ./lib/optee_armtz/b689f2a7-8adf-477a-9f99-32e90c0ad0a2.ta
    ./lib/optee_armtz/2a287631-de1b-4fdd-a55c-b9312e40769a.ta
    ./lib/optee_armtz/ffd2bded-ab7d-4988-95ee-e4962fff7154.ta
    ./lib/optee_armtz/e626662e-c0e2-485c-b8c8-09fbce6edf3d.ta
    ./bin/
    ./bin/xtest
    ./usr/
    ./usr/lib/
    ./usr/lib/libteec.so.1.0.0
    ./usr/lib/tee-supplicant/
    ./usr/lib/tee-supplicant/plugins/
    ./usr/lib/tee-supplicant/plugins/f07bfc66-958c-4a15-99c0-260e4e7375dd.plugin
    ./usr/lib/libteec.a
    ./usr/lib/libteec.so
    ./usr/lib/libteec.so.1
    ./usr/lib/libckteec.a
    ./usr/lib/libteec.so.1.0
    ./usr/lib/libckteec.so
    ./usr/lib/libckteec.so.0.1.0
    ./usr/lib/libckteec.so.0
    ./usr/lib/libckteec.so.0.1
    ./usr/bin/
    ./usr/bin/optee_example_hello_world
    ./usr/bin/optee_example_acipher
    ./usr/bin/optee_example_secure_storage
    ./usr/bin/optee_example_aes
    ./usr/bin/optee_example_hotp
    ./usr/bin/optee_example_plugins
    ./usr/bin/optee_example_random
    ./usr/include/
    ./usr/include/pkcs11_ta.h
    ./usr/include/tee_plugin_method.h
    ./usr/include/tee_client_api.h
    ./usr/include/pkcs11.h
    ./usr/include/tee_bench.h
    ./usr/include/tee_client_api_extensions.h
    ./usr/include/ck_debug.h
    ./usr/include/optee_client_config.mk
    ./usr/include/teec_trace.h
    ./usr/sbin/
    ./usr/sbin/tee-supplicant

スクリプトを用いることで，一連の実行を自動化することができます．
実行前に，IPアドレスや名前が正しく設定されていることを確認してください．

.. code-block:: bash

    $ ./deploy.sh

.. attention::

    既存のスクリプトは， ``sshpass -p`` によって，パスワードの入力を省略していますが，セキュリティには十分な注意が必要です．
