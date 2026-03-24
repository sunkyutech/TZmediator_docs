#############
関連研究
#############

関連研究の探し方
**********************

.. hint::
    - Google Scholarで "TEE" などの関連キーワードを検索します．
    - 権威ある論文から　`CONECTED PAPERS <https://www.connectedpapers.com/>`_ を利用して関連した研究を探します．

関連研究を以下にまとめます．

TEEのサーベイ論文
***********************

Trusted Execution Environment（TEE）は，CPU内部に隔離された実行環境を提供し，
OSが侵害された場合でもコードとデータの機密性・完全性を保護する仕組みである．
TEEの設計や応用については多くのサーベイ研究が存在する．

.. list-table::
   :header-rows: 1

   * - タイトル
     - 著者
     - 年
     - 出版
     - 備考

   * - `A Survey of Secure Computation Using Trusted Execution Environments <https://arxiv.org/abs/2302.12150>`_
     - Xiaoguo Li, Bowen Zhao, Guomin Yang, Tao Xiang, Jian Weng, Robert H. Deng
     - 2023
     - arXiv
     - TEEを利用した安全計算プロトコルを分類し，セキュリティ・性能などの観点から比較

   * - `A Survey on the (In)Security of Trusted Execution Environments <https://www.sciencedirect.com/science/article/pii/S0167404823000901>`_
     - Alejandro Muñoz et al.
     - 2023
     - Computers & Security
     - TEEの脆弱性や攻撃手法を体系的に整理

   * - `An Exploratory Study of Attestation Mechanisms for Trusted Execution Environments <https://arxiv.org/abs/2204.06790>`_
     - J. Ménétrey et al.
     - 2022
     - arXiv
     - SGX，TrustZone，AMD SEVなどのリモートアテステーション方式を比較

   * - `A Comprehensive Analysis of Trusted Execution Environments`
     - Osama Hosameldeen, Fan BinYuan
     - 2022
     - IEEE
     - TEEの定義，アーキテクチャ，分類を整理した総合的サーベイ

   * - `A Survey of Intel SGX and Its Applications`
     - Wei Zheng et al.
     - 2021
     - Frontiers of Computer Science
     - Intel SGXの仕組みと応用を整理したサーベイ

   * - `A Survey of RISC-V Secure Enclaves and Trusted Execution Environments`
     - M. Boubakri et al.
     - 2025
     - Electronics (MDPI)
     - RISC-VベースのTEEおよびSecure Enclave研究の整理


POSIX API on TEE
****************

Intel SGX
=========

Intel SGXを対象とした研究では，既存アプリケーションを大きく変更せずに
TEE上で実行するために，POSIX APIやLinuxシステムコール互換の環境を提供する
研究が多く提案されている．これらの研究は，Library OSやランタイムを
enclave内に実装することで既存アプリケーションの移植性を高めることを
目的としている．

- `SCONE: Secure Linux Containers with Intel SGX <https://www.usenix.org/system/files/conference/osdi16/osdi16-arnautov.pdf>`_
    - Sergei Arnautov et al.
    - 12th USENIX Symposium on Operating Systems Design and Implementation (OSDI 16), pages 689-703, 2016. 
    - SGX上でLinuxコンテナを実行するためのランタイム．libcを改変しPOSIX APIを提供．

.. list-table::
   :header-rows: 1

   * - タイトル
     - 著者
     - 年
     - 出版
     - 備考

   * - `SCONE: Secure Linux Containers with Intel SGX <https://www.usenix.org/system/files/conference/osdi16/osdi16-arnautov.pdf>`_
     - Sergei Arnautov et al.
     - 2016
     - 12th USENIX Symposium on Operating Systems Design and Implementation (OSDI 16)
     - SGX上でLinuxコンテナを実行するためのランタイム．libcを改変しPOSIX APIを提供．

   * - `Graphene-SGX: A Practical Library OS for Unmodified Applications on Intel SGX <https://www.usenix.org/system/files/conference/atc17/atc17-tsai.pdf>`_
     - Chia-che Tsai, Donald E. Porter, Mona Vij
     - 2017
     - USENIX Annual Technical Conference (ATC 17)
     - Library OSにより既存LinuxアプリケーションをSGX上で実行可能にする．POSIX互換インタフェースを提供．

   * - `Occlum: Secure and Efficient Multitasking Inside a Single Enclave of Intel SGX <https://www.usenix.org/system/files/atc20-shen.pdf>`_
     - Jian Shen, Shuang Chen, et al.
     - 2020
     - USENIX Annual Technical Conference (ATC 20)
     - SGX enclave内でマルチプロセス実行を可能にするLibOS．Linux互換のPOSIX APIを提供．

   * - `Panoply: Low-TCB Linux Applications with SGX Enclaves <https://www.usenix.org/system/files/conference/ndss17/ndss17_06-3_shinde_paper.pdf>`_
     - Shweta Shinde et al.
     - 2017
     - Network and Distributed System Security Symposium (NDSS 2017)
     - LinuxアプリケーションをSGX上で実行するための分離アーキテクチャ．システムコールを分離してPOSIX互換を実現．

   * - `Haven: Shielding Applications from an Untrusted Cloud with Intel SGX <https://www.microsoft.com/en-us/research/wp-content/uploads/2016/02/haven.pdf>`_
     - Andrew Baumann et al.
     - 2014
     - 11th USENIX Symposium on Operating Systems Design and Implementation (OSDI 14)
     - SGX上でWindowsアプリケーションを実行するためのLibrary OS．Drawbridgeを利用．

Arm TrustZone
=============

Arm TrustZoneにおいても，既存アプリケーションを大きく変更せずに
セキュア環境で実行するために，POSIX API互換環境を提供する研究が
いくつか提案されている．これらの研究では，Trusted Application内に
ランタイムや軽量OSを実装することで，POSIX APIを利用したアプリケーションの
移植性を向上させることを目的としている．

.. list-table::
   :header-rows: 1

   * - タイトル
     - 著者
     - 年
     - 出版
     - 備考

   * - `eMCOS POSIX: A POSIX Compatible Operating System for Embedded Systems <https://www.esol.com/embedded/emcos-posix/>`_
     - eSOL Co., Ltd.
     - 2019
     - Product / Technical Report
     - Arm TrustZoneを利用したリアルタイムOS．POSIX互換インタフェースを提供し，セキュアアプリケーションを実行可能．

   * - `Tarnhelm: Secure and Efficient System Call Execution in TrustZone <https://dl.acm.org/doi/10.1145/3302424.3303977>`_
     - Johannes Winter et al.
     - 2019
     - Proceedings of the 14th ACM Asia Conference on Computer and Communications Security (AsiaCCS)
     - TrustZone環境で安全にシステムコールを処理する機構を提案．POSIX APIを安全に利用できるようにするための仕組みを提供．

   * - `Sirius: Efficient Application Isolation for TrustZone <https://www.usenix.org/system/files/sec19-park.pdf>`_
     - Jaehyun Park et al.
     - 2019
     - 28th USENIX Security Symposium
     - TrustZone上でアプリケーション分離を実現するフレームワーク．Linuxアプリケーションの実行を想定し，POSIX互換環境を提供．


WASIの拡張
******************

WebAssemblyの標準システムインタフェースである
WebAssembly System Interface（WASI）は，
ポータブルなシステムAPIを提供することを目的としている．
しかし，現行のWASIはPOSIX APIと比較して機能が限定されているため，
ネットワーク通信やスレッドなどの機能を拡張する研究が行われている．

.. list-table::
   :header-rows: 1

   * - タイトル
     - 著者
     - 年
     - 出版
     - 備考

   * - `WASIX: Extending WASI with Threading, Networking, and More <https://wasix.org/>`_
     - Syrus Akbary et al.
     - 2023
     - Wasmer Project
     - WASIを拡張し，スレッド，ソケット，fork，signalなどのPOSIX機能を提供する拡張仕様．

   * - `WALI: WebAssembly Lightweight Interface for POSIX Compatibility <https://dl.acm.org/doi/10.1145/3560837.3563847>`_
     - Yuta Nakajima et al.
     - 2022
     - ACM Middleware Workshop
     - WebAssembly環境でPOSIX互換APIを提供する軽量インタフェースを提案．

TAの分離・隔離
**********************

Trusted Execution Environmentでは，Trusted Application（TA）が
同一のTEE OS上で実行されることが多く，TEE OSが侵害された場合には
すべてのTAが影響を受ける可能性がある．
そのため，TEE内部においてもアプリケーションやサービスを分離し，
被害の影響範囲を限定することを目的とした研究が提案されている．
これらの研究では，TEEを複数の実行ドメインに分割する方式や，
軽量ランタイムを利用したアプリケーション隔離などが検討されている．

.. list-table::
   :header-rows: 1

   * - タイトル
     - 著者
     - 年
     - 出版
     - 備考

   * - `WaTZ: A Trusted WebAssembly Runtime Environment with Remote Attestation for TrustZone <https://arxiv.org/abs/2206.08722>`_
     - J. Ménétrey, A. Pasin, et al.
     - 2022
     - arXiv
     - TrustZone上でWebAssemblyアプリケーションを安全に実行するランタイムを提案．軽量なリモートアテステーション機構も提供． :contentReference[oaicite:0]{index=0}

   * - `ReZone: Disarming TrustZone with TEE Privilege Reduction <https://arxiv.org/abs/2203.01025>`_
     - David Cerdeira, José Martins, Nuno Santos, Sandro Pinto
     - 2022
     - USENIX Security
     - モノリシックTEEを複数のゾーンに分割し，Trusted OSの権限を削減することでTAの隔離を強化． :contentReference[oaicite:1]{index=1}

   * - `dTEE: Distributed Trusted Execution Environment <https://ieeexplore.ieee.org/document/10577323>`_
     - Simon Ott, Benjamin Orthen, Alexander Weidinger, Julian Horsch, Vijayanand Nayani, Jan-Erik Ekberg
     - 2024
     - ACM Asia Conference on Computer and Communications Security (AsiaCCS 2024)
     - 複数デバイス上のTEEを安全な通信路とリモートアテステーションにより連携させ，分散TEEを構築するアーキテクチャを提案．Trusted Application間で安全なデータ交換と協調処理を可能にする．

   * - `MicroTEE: Designing TEE OS Based on the Microkernel Architecture <https://arxiv.org/abs/1908.07159>`_
     - Dongxu Ji, Qianying Zhang, Shijun Zhao, Zhiping Shi, Yong Guan
     - 2019
     - arXiv
     - マイクロカーネル構造のTEE OSを提案し，サービスをユーザレイヤに分離することでTEE内部の分離性を向上． :contentReference[oaicite:2]{index=2}

   * - `PrivateZone: Providing a Private Execution Environment Using ARM TrustZone <https://dl.acm.org/doi/10.1145/3319535.3354217>`_
     - Jaehyun Park, Jaeyoung Choi, Sang-Han Lee, Ho-Young Lee
     - 2019
     - Proceedings of the 16th ACM International Conference on Mobile Systems, Applications, and Services (MobiSys 2019)
     - TrustZoneを利用してユーザごとに隔離された実行環境を提供するフレームワーク．ユーザのプロファイルやデータを分離して保護することを目的とする．


TrustZoneを活用したアプリケーション
******************************************

.. list-table::
   :header-rows: 1

   * - タイトル
     - 著者
     - 年
     - 出版
     - 備考

   * - `Using ARM TrustZone to Build a Trusted Language Runtime for Mobile Applications <https://www.microsoft.com/en-us/research/publication/using-arm-trustzone-build-trusted-language-runtime-mobile-applications/>`_
     - Nuno Santos, Himanshu Raj, Stefan Saroiu, Alec Wolman
     - 2014
     - 19th International Conference on Architectural Support for Programming Languages and Operating Systems (ASPLOS '14)
     - モバイルアプリ向けの Trusted Language Runtime（TLR）を提案．アプリケーションのセキュリティクリティカルな処理を TrustZone 上で実行する．

   * - `Trust-E: A Trusted Embedded Operating System Based on the ARM Trustzone <https://dl.acm.org/doi/10.1109/UIC-ATC-ScalCom.2014.15>`_
     - Xia Yang, Peng Shi, Bo Tian, Bing Zeng, Wei Xiao
     - 2014
     - IEEE UIC/ATC/ScalCom 2014
     - Arm TrustZone 上に構築した組込み向け trusted OS．モバイル決済アプリケーションをデモとして実装．

   * - `TrustOTP: Transforming Smartphones into Secure One-Time Password Tokens <https://dl.acm.org/doi/abs/10.1145/2810103.2813692>`_
     - He Sun, Kun Sun, Yuewu Wang, Jiwu Jing
     - 2015
     - 22nd ACM SIGSAC Conference on Computer and Communications Security (CCS 2015)
     - スマートフォンを TrustZone ベースの安全な OTP トークンとして利用する研究．

   * - `Hardware-Security Technologies for Industrial IoT: TrustZone and Security Controller <https://tugraz.elsevierpure.com/en/publications/hardware-security-technologies-for-industrial-iot-trustzone-and-s/>`_
     - Christian Lesjak, Daniel Hein, Johannes Winter
     - 2015
     - IECON 2015 - 41st Annual Conference of the IEEE Industrial Electronics Society
     - 産業 IoT 向けのデバイススナップショット認証を対象とした研究．TrustZone と Security Controller を比較している．

   * - `fTPM: A Software-Only Implementation of a TPM Chip <https://www.usenix.org/conference/usenixsecurity16/technical-sessions/presentation/raj>`_
     - Himanshu Raj, Stefan Saroiu, Alec Wolman, Jacob R. Lorch, Magnus Nystrom, David Robinson, Rob Spiger, Stefan Thom, David Wooten
     - 2016
     - 25th USENIX Security Symposium (USENIX Security 16)
     - TrustZone を用いた firmware TPM 2.0 実装．実運用されるセキュリティサービスの代表例．

   * - `ARM TrustZone for Secure Image Processing on the Cloud <https://syssec.dpss.inesc-id.pt/papers/brito_wmcsp16.pdf>`_
     - Tiago Brito, Nuno O. Duarte, Nuno Santos
     - 2016
     - IEEE International Workshop on Multimedia Content Protection and Security (WMCPS 2016)
     - Darkroom を提案．クラウド上で画像を安全に復号・変換・再暗号化する画像処理サービス．

   * - `PrivateZone: Providing a Private Execution Environment Using ARM TrustZone <https://pure.kaist.ac.kr/en/publications/privatezone-providing-a-private-execution-environment-using-arm-t/>`_
     - Jinsoo Jang, Changho Choi, Jaehyuk Lee, Nohyun Kwak, Seongman Lee, Yeseul Choi, Brent Byunghoon Kang
     - 2018
     - IEEE Transactions on Dependable and Secure Computing
     - 一般開発者が TrustZone を利用できるようにする Private Execution Environment を提供．モバイルアプリの保護を想定．

   * - `TrApps: Secure Compartments in the Evil Cloud <https://www.ibr.cs.tu-bs.de/users/brenner/papers/2017-xdom0-trapps.pdf>`_
     - Stefan Brenner, David Goltzsche, Rüdiger Kapitza
     - 2017
     - XDOM0'17: Workshop on Security and Dependability of Multi-Domain Infrastructures
     - TrustZone を用いたクラウド向けの分散アプリケーション実行基盤．分割アプリケーションの security-sensitive component を secure world で実行する．

   * - `OPTZ: a Hardware Isolation Architecture of Multi-Tasks Based on TrustZone Support <https://www.researchgate.net/publication/325423602_OPTZ_a_Hardware_Isolation_Architecture_of_Multi-Tasks_Based_on_TrustZone_Support>`_
     - Hongjun Dai, Kang Chen
     - 2017
     - IEEE ISPA/IUCC 2017
     - マルチタスク環境を想定した TrustZone ベースのハードウェア分離アーキテクチャ．

   * - `TM-Coin: Trustworthy Management of TCB Measurements in IoT <https://www.computer.org/csdl/proceedings-article/percom-workshops/2017/07917640/19wAG9qgidi>`_
     - Jaemin Park, Kwangjo Kim
     - 2017
     - IEEE PerCom Workshops 2017
     - IoT における TCB 計測値の信頼管理を対象とした研究．remote attestation の管理面を強化する．

   * - `Secure Edge Computing with ARM TrustZone <https://www.scitepress.org/PublishedPapers/2017/63086/63086.pdf>`_
     - Robert Pettersen, Håvard D. Johansen, Dag Johansen
     - 2017
     - 2nd International Conference on Internet of Things, Big Data and Security (IoTBDS 2017)
     - エッジ−フォグ−クラウドをまたぐ TrustZone/SGX ベースの安全なエッジコンピューティング基盤を提案．

   * - `TruApp: A TrustZone-based Authenticity Detection Service for Mobile Apps <https://www.dpss.inesc-id.pt/~mpc/pubs/truapp-final.pdf>`_
     - Sileshi Demesie Yalew, Pedro Mendonça, Gerald Q. Maguire Jr., Seif Haridi, Miguel Correia
     - 2017
     - 13th IEEE International Conference on Wireless and Mobile Computing, Networking and Communications (WiMob 2017)
     - モバイルアプリの真正性・完全性検証を TrustZone で支援するサービス．

   * - `TrustShadow: Secure Execution of Unmodified Applications with ARM TrustZone <https://dl.acm.org/doi/10.1145/3081333.3081349>`_
     - Le Guan, Peng Liu, Xinyu Xing, Xinyang Ge, Shengzhi Zhang, Meng Yu, Trent Jaeger
     - 2017
     - 15th Annual International Conference on Mobile Systems, Applications, and Services (MobiSys 2017)
     - 既存アプリケーションを大きく変更せずに TrustZone 上で保護実行するシステム．IoT/edge 上の legacy application の保護に近い．

   * - `StreamBox-TZ: Secure Stream Analytics at the Edge with TrustZone <https://www.usenix.org/conference/atc19/presentation/park-heejin>`_
     - Heejin Park, Shoumeng Zhai, Long Lu, Felix Xiaozhu Lin
     - 2019
     - USENIX Annual Technical Conference (USENIX ATC 19)
     - TrustZone を活用したエッジ向けストリーム解析基盤．データ保護と結果の検証可能性を両立する．

   * - `LEAP: TrustZone Based Developer-Friendly TEE for Intelligent Mobile Apps <https://www.computer.org/csdl/journal/tm/2023/12/09895274/1GNpcQQdZ4Y>`_
     - Lizhi Sun, Shuocheng Wang, Hao Wu, Yuhang Gong, Fengyuan Xu, Yunxin Liu, Hao Han, Sheng Zhong
     - 2023
     - IEEE Transactions on Mobile Computing
     - インテリジェントモバイルアプリ向けの開発者フレンドリーな TrustZone 実行基盤．GPU 利用や並列実行を支援する．

   * - `KeVlar-Tz: A Secure Cache for Arm TrustZone <https://link.springer.com/chapter/10.1007/978-3-030-78198-9_8>`_
     - Oscar Benedito, Ricard Delgado-Gonzalo, Valerio Schiavoni
     - 2021
     - Distributed Applications and Interoperable Systems (DAIS 2021)
     - OP-TEE 上で実装した TrustZone ベースのセキュアキャッシュ．ヘルスケア・ウェアラブル等の機微データ保存を想定．

   * - `CamShield: Securing Smart Cameras through Physical Replication and Isolation <https://www.usenix.org/conference/usenixsecurity22/presentation/wang-zhiwei>`_
     - Zhiwei Wang, Yihui Yan, Yueli Yan, Huangxun Chen, Zhice Yang
     - 2022
     - 31st USENIX Security Symposium (USENIX Security 22)
     - スマートカメラのプライバシ保護を目的としたシステム．TrustZone と外付けデバイスを組み合わせて映像取得経路を保護する．

   * - `RT-TEE: Real-time System Availability for Cyber-physical Systems using ARM TrustZone <https://www.cse.wustl.edu/~lu/papers/sp22-rt-tee.pdf>`_
     - Jinwen Wang, Ao Li, Haoran Li, Chenyang Lu, Ning Zhang
     - 2022
     - IEEE Symposium on Security and Privacy (IEEE S&P 2022)
     - サイバーフィジカルシステム向けに，TrustZone を用いてリアルタイム性と可用性を両立する実行基盤を提案．

   * - `Confidential Execution of Deep Learning Inference at the Untrusted Edge with ARM TrustZone <https://dl.acm.org/doi/10.1145/3577923.3583648>`_
     - Md Shihabul Islam, Mahmoud Zamani, Chung Hwan Kim, Latifur Khan, Kevin W. Hamlen
     - 2023
     - 13th ACM Conference on Data and Application Security and Privacy (CODASPY '23)
     - エッジ上の深層学習推論を TrustZone で保護する研究．モデルと入力データの機密性・完全性を対象とする．

   * - `SelTZ: Fine-Grained Data Protection for Edge Neural Networks Using Selective TrustZone Execution <https://www.mdpi.com/2079-9292/14/1/123>`_
     - Seunguk Jeong, Hyunyoung Oh
     - 2024
     - Electronics
     - ニューラルネットワーク全体ではなく，機微な部分だけを選択的に TrustZone で保護する手法．

   * - `On Practicality of Using ARM TrustZone Trusted Execution Environment for Securing Programmable Logic Controllers <https://dl.acm.org/doi/10.1145/3634737.3645002>`_
     - Zhiang Li, Daisuke Mashima, Wen Shei Ong, Ertem Esiner, Zbigniew Kalbarczyk, Ee-Chien Chang
     - 2024
     - ACM/IEEE International Conference on Cyber-Physical Systems (ICCPS 2024)
     - TEE-PLC を実装し，PLC の制御ロジック実行を TrustZone で保護できるかを検証した研究．
