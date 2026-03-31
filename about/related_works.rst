#############
関連研究
#############

関連研究の探し方
**********************

.. hint::
    
    - Google Scholarで "TEE" や "Arm TrustZone" などの関連キーワードを検索します．
    - 権威ある論文から　`CONECTED PAPERS <https://www.connectedpapers.com/>`_ を利用して類似した研究を探します．
        - ○の大きさは被引用数を表し，色の濃さは年数 (濃い方が比較的に新しい) 表します．
        - Connected Papers は引用ツリーではありません．そのため，直接的に引用関係にない論文も類似性が高ければ密接に配置されます．

関連研究を以下にまとめます．


TEEのサーベイ論文
***********************

TEEの設計や応用については多くのサーベイ研究が存在します．

- `Confidential Computing for Cloud Security: Exploring Hardware based Encryption Using Trusted Execution Environments <https://arxiv.org/pdf/2511.04550>`_
    - Dhruv Deepak Agarwal, Aswani Kumar Cherukuri
    - ArXiv, 2025.
    - 直近のサーベイ論文．


POSIX API on TEE
****************

TEE内で既存のアプリケーションを実行するために，POSIX APIやLinuxシステムコール互換の環境を提供する研究が多く提案されています．

Intel SGX
=========

Intel SGXを対象とした研究では，既存アプリケーションを大きく変更せずにTEE上で実行するために，POSIX APIやLinuxシステムコール互換の環境を提供する研究が多く提案されています．
これらの研究の多くは，ライブラリOSやランタイムをエンクレイヴ内に実装することで既存アプリケーションの移植性を高めることを目的としています．

- `SCONE: Secure Linux Containers with Intel SGX <https://www.usenix.org/system/files/conference/osdi16/osdi16-arnautov.pdf>`_
    - Sergei Arnautov, Bohdan Trach, Franz Gregor, Thomas Knauth, Andre Martin, Christian Priebe, Joshua Lind, Divya Muthukumaran, Dan O’Keeffe, Mark L Stillwell, David Goltzsche, David Eyers, Rudiger Kapitza, Peter Pietzuch, Christof Fetzer
    - 12th USENIX Symposium on Operating Systems Design and Implementation (OSDI 16), pages 689-703, 2016. 
    - SGX上でLinuxコンテナを実行するためのランタイム．libcを改変しPOSIX APIを提供．

- `Graphene-SGX: A Practical Library OS for Unmodified Applications on Intel SGX <https://www.usenix.org/system/files/conference/atc17/atc17-tsai.pdf>`_
    - Chia-che Tsai, Donald E. Porter, Mona Vij
    - USENIX Annual Technical Conference (ATC 17), pages 645 - 658, 2017.
    - ライブラリOSにより既存LinuxアプリケーションをSGX上で実行可能にする．POSIX互換インタフェースを提供．

- `Occlum: Secure and Efficient Multitasking Inside a Single Enclave of Intel SGX <https://dl.acm.org/doi/epdf/10.1145/3373376.3378469>`_
    - Youren Shen, Hongliang Tian, Yu Chen, Kang Chen, Runji Wang, Yi Xu, Yubin Xia and Shoumeng Yan
    - Proceedings of the Twenty-Fifth International Conference on Architectural Support for Programming Languages and Operating Systems (ASPLOS 20), pages 955-970, 2020.
    - エンクレイヴ内でマルチプロセス実行を可能にするライブラリOS．Linux互換のPOSIX APIを提供．

- `Panoply: Low-TCB Linux Applications with SGX Enclaves <https://www.usenix.org/system/files/conference/ndss17/ndss17_06-3_shinde_paper.pdf>`_
   - Shweta Shinde, Dat Le Tien, Shruti Tople, Prateek Saxena
   - Network and Distributed System Security Symposium (NDSS 2017), 2017.
   - LinuxアプリケーションをSGX上で実行するための分離アーキテクチャ．

- `Shielding Applications from an Untrusted Cloud with Haven <https://dl.acm.org/doi/epdf/10.1145/2799647>`_
   - Andrew Baumann, Marcus Peinado and Galen Hunt
   - ACM Transactions on Computer Systems (TOCS), Volume 33, Issue 3, pages 1 - 26, 2015.
   - SGX上でWindowsアプリケーションを実行するためのライブラリOS．


Arm TrustZone
=============

Arm TrustZoneにおいても，セキュアワールドで既存のアプリケーションを実行するために，POSIX API互換環境を提供する研究がいくつか提案されている．

- `eMCOS POSIX <https://www.esol.co.jp/embedded/product/emcos-posix_overview.html>`_
    - eSOL Co., Ltd.
    - Product, 2019.
    - Arm TrustZoneを利用したリアルタイムOS．POSIX互換インタフェースを提供．

- `Tarnhelm: Isolated, Transparent & Confidential Execution of Arbitrary Code in ARM's TrustZone <https://dl.acm.org/doi/10.1145/3302424.3303977>`_
    - Davide Quarta, Michele Ianni, Aravind Machiry, Yanick Fratantonio, Eric Gustafson, Davide Balzarotti, Martina Lindorfer, Giovanni Vigna and Christopher Kruegel
    - Proceedings of the 2021 Research on offensive and defensive techniques in the Context of Man At The End (MATE) Attacks (Checkmate 21), pages 43 - 57, 2019.
    - セキュアワールドからで安全にシステムコールを処理する機構を提案．

- `Sirius: Enabling System-Wide Isolation for Trusted Execution Environments <https://arxiv.org/pdf/2009.01869v1>`_
     - Zahra Tarkhani, Anil Madhavapeddy
     - ArXiv, 2020.
     - OP-TEEを用いて実装し，LMbenchを実行．


WASIの拡張
******************

WebAssembly (Wasm) の標準システムインタフェースであるWebAssembly System Interface (WASI) は，ポータブルなシステムAPIを提供することを目的としているが，現行のWASIはPOSIX APIと比較して機能が限定的である．
そこで，POSIX互換性を高めたり，Linuxアプリケーションを実行するための拡張仕様が提案されている．

`WASIX <https://wasix.org/>`_
    - Wasmer Inc.
    - Wasmer Project.
    - WASIを拡張し，スレッド，ソケット，fork，シグナルなどのPOSIX機能を提供する拡張仕様．

- `Empowering WebAssembly with Thin Kernel Interfaces <https://dl.acm.org/doi/epdf/10.1145/3689031.3717470>`_
    - Arjun Ramesh, Tianshu Huang, Ben L. Titzer and Anthony Rowe
    - Proceedings of the Twentieth European Conference on Computer Systems (EuroSys 25), pages 1 - 20, 2022.
    - WebAssembly環境でPOSIX互換APIを提供する抽象化レイヤを提案．


TAの分離・隔離
**********************

セキュアワールドでは，TAが同一の実行環境で動作するため，Trusted OSが侵害されると，他のTAにも影響を及ぼす恐れがある．
そのため，セキュアワールド内部においてもアプリケーションやサービスを分離し，被害の影響範囲を限定することを目的とした研究が提案されている．
また，アプリケーションをCAとTAに自動で分割して実行することで，攻撃対象を減らすアプローチも存在する．

- `WaTZ: A Trusted WebAssembly Runtime Environment with Remote Attestation for TrustZone <https://arxiv.org/abs/2206.08722>`_
    - Jämes Ménétrey, Marcelo Pasin, Pascal Felber, Valerio Schiavoni
    - IEEE 42nd International Conference on Distributed Computing Systems (ICDCS 2022), pages 1177 - 1189, 2022.
    - TrustZone上でWasmアプリケーションを安全に実行するランタイムを提案．軽量なリモートアテステーション機構も提供．

- `ReZone: Disarming TrustZone with TEE Privilege Reduction <https://www.usenix.org/system/files/sec22-cerdeira.pdf>`_
    - David Cerdeira, José Martins, Nuno Santos, Sandro Pinto
    - 31st USENIX Security Symposium (USENIX Security 22), pages 2261 - 2279, 2022.
    - TAとTrusted OSを複数のゾーンに分割し，Trusted OSの権限を削減することでTAの隔離を強化．

- dTEE: A Declarative Approach to Secure IoT Applications Using TrustZone
    - Tong Sun, Borui Li, Yixiao Teng, Yi Gao, Wei Dong
    - IEEE International Conference on Information Processing in Sensor Networks (IPSN 2024), pages 200 - 212, 2024.
    - IoTアプリケーションをCAとTAに自動で分割して実行するフレームワーク．
