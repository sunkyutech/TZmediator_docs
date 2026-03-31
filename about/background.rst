##################
背景 (Key words)
##################

ここでは，TZmediatorに関連する技術や概念について説明します．
詳細な説明は，修論の第2章を参照してください．

**Trusted Execution Environment (TEE)**

Trusted Execution Environment (TEE) は，CPUが提供する隔離実行環境であり，OSなどから独立して安全にコードとデータを処理できます．
TEE内で実行される処理は，OSを含む他のソフトウェアからアクセスできません．
代表的なTEEアーキテクチャとして，アプリケーション向けのIntel SGX，Arm TrustZone，RISC-V Keystone，仮想マシン向けのAMD SEV，Intel TDX，Arm CCAなどがあります．
TEEを用いることで，OSやハイパーバイザが侵害された場合でもエッジデバイスで動作するクラウドアプリケーションを保護することができます．

**Arm TrustZone**

Arm TrustZoneは，Armプロセッサが提供するTEE技術であり，システムをセキュアワールドとノーマルワールドの2つのワールド (実行環境) に分割します．
セキュアワールドではTrusted Application (TA) が実行され，機密情報の処理やセキュリティクリティカルな処理を担当します．
ノーマルワールドでは通常のOSやTAを実行するためのアプリケーション (Client Application，CA) が実行されます．
ワールド間の通信は専用のインタフェースを介して行われます．

**OP-TEE**

OP-TEE (Open Portable Trusted Execution Environment) は，Arm TrustZone向けのオープンソースソフトウェアであるTEEの実装です．
セキュアワールドで動作するTrusted OS (OP-TEE OS) と，ノーマルワールドから呼び出すためのクライアントライブラリを提供します．
GlobalPlatformの仕様に準拠したAPIをサポートしています．

**GlobalPlatform API**

GlobalPlatform APIは，TEEにおける標準化されたプログラミングインタフェースです．
主に以下の2種類があります．

- TEE Client API (CA側) 
- TEE Internal Core API (TA側) 

これらのAPIにより，CAからTAを呼び出したり，TA内でセキュアな処理を実行できたりします．

**POSIX API**

POSIX APIは，Unix系OSで広く利用される標準的なライブラリインタフェース群です．
ファイル操作，プロセス管理，スレッド，ソケット通信などの機能を統一的に提供します．

**WebAssembly (Wasm)**

WebAssembly (Wasm) は，軽量でポータブルなバイナリ形式の仮想マシン命令セットです．
ブラウザだけでなく，サーバやエッジデバイスでも実行可能であり，安全なサンドボックス環境で動作します．
ネイティブコードに近い性能を持ちながら，高い移植性と安全性を両立する点が特徴です．

**WebAssembly System Interface (WASI)**

WebAssembly System Interface (WASI) は，WebAssemblyに対してOS機能を提供する標準インタフェースです．
ファイルI/Oや環境変数などの基本機能を提供しますが，2026年時点ではPOSIX APIと比較して機能が限定されています．
