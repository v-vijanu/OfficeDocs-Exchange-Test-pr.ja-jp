﻿---
title: 'ボイス メール ユーザーが FAX を受信できるようにする: Exchange 2013 Help'
TOCTitle: ボイス メール ユーザーが FAX を受信できるようにする
ms:assetid: 451ab0ea-21e1-4c1f-ae62-4ba7cdfd1e4d
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb232022(v=EXCHG.150)
ms:contentKeyID: 52057820
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ボイス メール ユーザーが FAX を受信できるようにする

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**トピックの最終更新日:** 2015-04-07_

Microsoft Exchange Unified Messaging (UM) を使用すると、ボイス メール メッセージをユーザーのメールボックスに配信したり、ユーザーが FAX メッセージを自分のメールボックスで受信できるようにしたりすることができます。UM では、FAX は .tif 拡張子のイメージ ファイルが添付された電子メール メッセージとしてユーザーのメールボックスに送信されます。ユーザーは, .tif 拡張子のイメージ ファイルを開いて表示できるソフトウェア アプリケーションを使用して、添付ファイルを開くことができます。ここでは、FAX の送受信、および UM の FAX 送受信のしくみについて説明します。


> [!NOTE]
> ユーザーは、ユニファイド メッセージングでは FAX を送信できませんが、インターネット FAX サービス、電子メール FAX サービス、サード パーティ FAX サーバー アプリケーションなどの多くのサード パーティ ソリューションを使用することにより FAX を送信できます。



**目次**

FAX 送受信の概要

FAX 送受信の方法

T.38

ユニファイド メッセージングによる FAX 送受信の概要

着信 FAX の受信

FAX 呼び出しの参照方法

FAX 送受信の構成

電話番号と FAX 送受信

UM FAX メッセージのジャーナリング

## FAX 送受信の概要

FAX は facsimile (ファクシミリ) の短縮形であり、ドキュメントの電子的な転送に使用されるテクノロジです。FAX は、一般にテレフォニーまたは回線ベースのネットワークである公衆交換電話網 (PSTN) を使用して、FAX マシンまたはコンピューターの FAX モデムによって送受信されます。ただし、その他のオプションも、FAX の送受信に使用できます。

現在、ほとんどすべての組織で、ユーザーが FAX を送受信できる必要があります。組織では、以下に記載する 1 つ以上の方法を使用して、PSTN またはインターネットを介して FAX を送受信しています。これらの方法にはそれぞれ長所と短所があります。

  - 従来の FAX マシンおよびコンピューター ベースでの FAX 送受信

  - FAX サーバーまたは FAX ゲートウェイを使用した FAX 送受信

  - ボイス オーバー IP (VoIP) ネットワークを使用した FAX 送受信

  - 電子メール クライアント アプリケーションを使用した FAX 送受信

FAX メッセージを送信するには、組織内のユーザーは次の操作を行う必要があります。

  - FAX 送信するドキュメントのハード コピーを印刷し、物理的な FAX マシンを使用して送信する。

  - コンピューターにドキュメントを保存し、FAX モデムを使用して FAX を送信しますが、そのためにはコンピューターに電話線を接続する必要があります。

  - ベンダー固有のソフトウェア アプリケーションからドキュメントを FAX 送信できるインターネット FAX サービスを使用します。

  - FAX サーバーを使用するように構成されているソフトウェア アプリケーションを使用して、FAX サーバーに FAX を送信する。

FAX を受信するには、組織内のユーザーは次の操作を行う必要があります。

  - 組織内の物理的な FAX マシンで FAX を受信する。

  - コンピューターにインストールされている FAX モデムを使用して FAX を受信する。

  - インターネット FAX サービスから FAX を受信する。

  - ネットワーク上に構成されている FAX サーバーから FAX を受信する。

  - ユニファイド メッセージングを使用する FAX パートナーのサーバーから FAX を受信します。このサーバーは VoIP ネットワークを使用して FAX を配信します。

ページのトップへ

## FAX 送受信の方法

FAX を送受信するためのオプションは、以下に示すように複数あります。

**従来の FAX マシンおよびコンピューター ベースでの FAX 送受信**   スキャナー、コンピューターの FAX モデム、FAX 機能が組み込まれたプリンター、または専用の FAX マシンを使用して FAX を送受信できます。これらを使用すると、電話回線を使用してデータをパルス形式で別の FAX デバイス (通常は別の FAX マシンまたは FAX モデムがインストールされているコンピューター) に送信できます。送信されたパルスは、イメージに変換されるか、用紙にイメージを印刷するために使用されます。

従来の FAX 送受信方法では、送受信デバイスに少なくとも 1 つの電話回線が必要で、一度に送信または受信できる FAX は 1 つだけです。FAX モデムを使用した FAX 送受信の短所は、コンピューターが、電源がオンになっていて FAX ソフトウェアまたは FAX サービスを実行している必要があることです。この種類のコンピューター ベースの FAX 送受信では、インターネットは使用されません。

**従来の FAX 送受信とコンピューター ベースの FAX 送受信**

![従来の FAX マシン](images/Bb232022.7bdc1cab-9504-4314-a6e0-eccdfe2a9cd6(EXCHG.150).gif "従来の FAX マシン")

**FAX サーバーまたは FAX ゲートウェイ、およびインターネット FAX サービス**   インターネットを介して FAX を送受信する方法は複数あります。コンピューターでソフトウェア アプリケーションを使用する方法や、電子メール クライアントを使用して FAX を受信する方法もこれに含まれます。この種類の送受信方法ではほとんどの場合、FAX サーバーまたは FAX ゲートウェイを使用して FAX と電子メールの間の変換を行います。組織で FAX マシンを撤去できるほか、追加の FAX マシンを購入する必要がないため、この方法は急速に普及しています。この方法では、電話回線を増設する必要もありません。この種類の送受信方法では、ドキュメントを作成し、正しい識別情報を記入した送付状を付けて、従来の FAX マシンに送信します。たとえば、ユーザーは Microsoft Word や Microsoft Outlook などのソフトウェア アプリケーションを使用して FAX を作成し、FAX サーバーまたは FAX ゲートウェイに送信します。FAX サーバーまたは FAX ゲートウェイは FAX を受信し、従来の電話回線を使用して FAX マシンまたはコンピューターにインストールされている FAX モデムに送信します。

**FAX サーバーまたは FAX ゲートウェイを使用した FAX 送受信**

![FAX サーバーまたは FAX ゲートウェイを使用した FAX 送受信](images/Bb232022.d6fa2402-b4ca-4313-956c-62e5fe7731ad(EXCHG.150).gif "FAX サーバーまたは FAX ゲートウェイを使用した FAX 送受信")

インターネット FAX サービスにより、ユーザーはインターネットを使用してコンピューターから FAX を送信できます。Word や Outlook などのソフトウェア アプリケーションを使用して、FAX を作成し、インターネット FAX サービスに送信できます。多くの企業が、サブスクリプション ベース、または FAX メッセージの送信ごとに料金が発生するシステムで、インターネット FAX サービスを提供しています。インターネット FAX サービスには次の長所があります。

  - FAX マシンが不要である。

  - ソフトウェアまたはハードウェアをインストールする必要がない。

  - 専用電話回線が不要である。

  - 機密を保持しやすい。

  - 同時に複数の FAX を送信できる。

  - コンピューターの電源がオフのときも FAX を受信できる。

次の図は、インターネット FAX サービスを使用して FAX を送受信する方法を示しています。

**インターネット FAX サービス**

![インターネット FAX サービス](images/Bb232022.5d0fb3d6-95f4-4fbf-80e5-64f5de553e65(EXCHG.150).gif "インターネット FAX サービス")

**電子メール クライアント アプリケーションを使用した FAX 送受信**   インターネットを介して FAX マシンで FAX を送受信し、それを Outlook などの電子メール クライアントで受信できます。

FAX マシンがインターネットを介して FAX メッセージを電子メール クライアントに送信できるようにするために、T.37 プロトコルが設計されました。FAX は、インターネットを介して電子メールの添付ファイル (通常は .tif ファイルまたは .pdf ファイル) として送信されます。この種類の FAX 送受信方法では、送信 FAX マシンと受信 FAX マシン用の電子メール アドレスに加えて、iFax または T.37 をサポートする FAX マシンが必要です。すべての T.37 FAX マシンは、従来の FAX マシンおよび FAX モデムと共に使用できるように、電話回線を使用した標準 FAX 送受信をサポートします。ただし場合によっては、FAX ゲートウェイを使用しているときに T.37 FAX マシンも使用できます。次の図は、T.37 ベースの FAX マシンと電子メール クライアントを使用して FAX を送受信する方法を示しています。

**電子メールによる FAX**

![電子メールによる FAX](images/Bb232022.086f086b-dc39-4439-a694-7a98e03e65d1(EXCHG.150).gif "電子メールによる FAX")

**VoIP ネットワークを使用した FAX 送受信**   VoIP は、ユーザーが IP ベースのネットワークを電話呼び出しの転送メディアとして利用できるようにするためのハードウェアとソフトウェアを提供するテクノロジです。VoIP ネットワークでは、音声データと FAX データは従来の回線転送 (PSTN の回線交換電話回線) ではなく IP を使用してパケットで送信されます。IP ネットワークと接続する VoIP ゲートウェイは VoIP を使用して、Microsoft Exchange Unified Messaging 呼び出しルーター サービスを実行しているクライアント アクセス サーバーと、Microsoft Exchange Unified Messaging Service および PBX (構内交換機) システムを実行しているメールボックス サーバーの間で、音声データ パケットを送信します。または IP PBX を使用して、VoIP ゲートウェイと PBX の両方の機能を実行することもできます。

ネットワークには、回線交換網とパケット交換網の 2 つの基本的な種類があります。回線交換網は、専用接続が存在するネットワークです。専用接続とは、2 つのノード間で通信できるようセットアップされた回線またはチャネルのことです。2 ノード間で呼び出しが確立すると、接続はこれらの 2 ノード間の専用接続として使用できます。一方のノードが呼び出しを終了すると、接続は取り消されます。PSTN などの回線交換網では、複数の呼び出しが同じ転送メディアを経由して転送されます。多くの場合、PSTN に使用されるメディアは銅線です。ただし、光ファイバー ケーブルが使用されることもあります。

インターネットやローカル エリア ネットワーク (LAN) などのパケット交換網では、パケットは最も効率のよいルートを経由して送信先に送信されますが、たとえ単一のメッセージを分割したパケットであっても、2 つのホスト間で転送されるパケットがすべて同じルートを通過するとは限りません。このため、ほぼ確実に各パケットの到着時間は異なり、到着する順番も異なります。パケット交換網では、パケット (メッセージまたはメッセージの断片) は、他のノードによって共有される可能性のあるデータ リンクを経由してノード間を個別にルーティングされます。パケット交換の場合は、回線交換とは異なり、ネットワーク上の複数のノード接続が使用可能な帯域幅を共有します。パケット交換網によってインターネットが存在できるようになり、それと同時に、データ ネットワーク、特に LAN ベースの IP ネットワークと VoIP ネットワークの利用も増え、普及しました。

ページのトップへ

## T.38

T.38 は、IP ベースのネットワークを介して FAX を使用できるようにする FAX 標準およびプロトコルです。T.38 プロトコルを使用する IP ベースのネットワークは、SMTP (簡易メール転送プロトコル) および MIME (Multipurpose Internet Mail Extension) を使用してメッセージを受信者のメールボックスに送信します。T.38 は、IP に対応した FAX デバイスおよび FAX ゲートウェイの IP FAX 転送を可能にします。このようなデバイスには、クライアント コンピューターやプリンターなどの IP ネットワークベースのホストが含まれます。Exchange Unified Messaging では、FAX イメージは, .tif ファイルとしてエンコードされ、電子メール メッセージに添付される個別のドキュメントです。電子メール メッセージと .tif 添付ファイルの両方が、ユーザーの UM が有効なメールボックスに送信されます。

ユニファイド メッセージングは、ゲートウェイの機能を使用して、PBX からの総合デジタル通信網 (ISDN) や QSIG などの時分割多重方式 (TDM) または電話回線交換型プロトコルを、セッション開始プロトコル (SIP)、リアルタイム転送プロトコル (RTP)、FAX メッセージ受信用の T.38 などの、IP または VoIP ベースのプロトコルに変換します。VoIP ゲートウェイは、ユニファイド メッセージングの機能と運用にとって不可欠です。VoIP ゲートウェイは FAX トーンを検出します。クライアント アクセス サーバーおよびメールボックス サーバーは、VoIP ゲートウェイを使用して、FAX が検出されたことを示す通知を送信します。その時点でクライアント アクセス サーバーおよびメールボックス サーバーはメディア セッションと再度ネゴシエートし、T.38 プロトコルを使用します。

ページのトップへ

## ユニファイド メッセージングによる FAX 送受信の概要

ユニファイド メッセージングでは、ユーザーは FAX イメージを, .tif イメージ ファイルとしてエンコードされ、電子メール メッセージに添付される個別のドキュメントとして受信します。電子メール メッセージと .tif 添付ファイルの両方が、ユーザーの UM が有効なメールボックスに送信されます。

FAX メッセージをユーザーのメールボックスに送信することには複数の利点があります。利点を以下に示します。

  - 物理的な FAX マシン、または従来の FAX マシンの数を減らすことができる。

  - メールボックス サーバーは多くの FAX をキューに入れ、電話回線のいずれかが空いたときにそれぞれの FAX を送信することができるため、組織内で FAX 送受信に使用する電話回線の数を減らすことができる。

  - .tif イメージ ファイルとして受信される FAX は、従来の FAX より高品質である。着信 FAX は、ローカル プリンターまたは共有プリンターで印刷できる。

  - ユーザーのメールボックスに送信される FAX は、受信者以外の人が取得する可能性がハード コピーの FAX より低いため、セキュリティが高まる。

  - ユーザーが、デスクを離れずに FAX を受信できる。

  - 受信する FAX メッセージを監視して、組織のセキュリティ ポリシーに準拠していることを確認できる。

1 つの FAX メッセージは、1 人の UM が有効なユーザーにのみ送信できます。ユニファイド メッセージングは、FAX メッセージを配布リストに転送できません。この機能が必要な場合は、次の手順を実行する必要があります。

1.  FAX 呼び出しに応答するためのメールボックスを作成します。これが配布リスト用のメールボックスになります。

2.  配布リスト メールボックスを UM が有効なメールボックスにします。

3.  この UM が有効なメールボックスのルールを作成します。ルールは、すべてのメッセージを選択した配布リストに転送するように構成されます。

ページのトップへ

## 着信 FAX の受信

VoIP ネットワークでの FAX 受信は、標準の FAX マシンでの FAX 受信や IP ベースのネットワーク上に配置されている FAX サーバーを使用した FAX 受信とは異なります。VoIP ネットワークを介して FAX を送受信できるようにするには、T.38 プロトコルをサポートする VoIP ゲートウェイまたは IP PBX と、同じく T.38 をサポートするサーバーが必要です。T.38 により、IP ネットワーク ベースのホスト (クライアント コンピューター、FAX 機能が組み込まれたプリンター、メールボックス サーバーなどのサーバーなど) に対する IP ベースの FAX 送信が可能になります。


> [!IMPORTANT]
> T.38 または G.711 を使用した FAX の送受信は、ユニファイド メッセージングと Microsoft Office Communications Server 2007 R2 または Microsoft Lync Server が統合された環境ではサポートされていません。



PBX は、呼び出しを受信するとそれを適切な内線に転送します。ユーザーの内線番号を呼び出しても応答がない場合、PBX はその呼び出しを VoIP ゲートウェイに転送し、ゲートウェイは呼び出しを適切なメールボックス サーバーに転送します。メールボックス サーバーは、呼び出しに使用されているプロトコルによって、その呼び出しが音声通話か FAX 通話かを判断します。SIP プロトコルが使用されている場合、メールボックス サーバーは呼び出しを音声メッセージとして処理します。ただし、VoIP ゲートウェイから T.38 プロトコルが使用されている場合、メールボックス サーバーは呼び出しが FAX であると認識し、以下のようにそれを処理します。メールボックス サーバーは、受信 FAX 呼び出しを専門の FAX パートナー サーバーに転送します。この FAX パートナー サーバーは、FAX 送信者との FAX 通話を確立し、UM が有効なユーザーの代わりに FAX を受信します。次に、FAX パートナーのサーバーは、SMTP メッセージに .tif 添付ファイルとして含まれている FAX を受信者のメールボックスに送信します。

メールボックス サーバーが VoIP ゲートウェイからの着信 T.38 FAX 信号を受信すると、メールボックス サーバーは、LDAP (ライトウェイト ディレクトリ アクセス プロトコル) を使用してディレクトリにクエリし、着信 FAX 呼び出しの意図した受信者に着信 FAX メッセージを受信するためのアクセス許可があるかどうか、および FAX パートナー サーバーの SIP アドレスを判断します。この情報を確認した後、メールボックス サーバーが FAX 呼び出し参照要求を VoIP ゲートウェイまたは SIP ピアに送信します。FAX 要求は次に FAX パートナー サーバーに転送されます。FAX 呼び出しが正常に確立されると、FAX 送信者が FAX メディアおよびデータを FAX パートナー サーバーに送信します。FAX パートナー サーバーは、FAX メディアとデータを受信した後、SMTP を使用してメールボックス サーバーに電子メール メッセージを送信します。このメッセージには、FAX メッセージの .tif イメージと、FAX の受信者を示す特殊なX-Header が含まれます。

FAX メッセージが認証され、有効な FAX パートナー サーバーから送信されると、メールボックス サーバー上の UM メールボックス アシスタントが RPC 呼び出しを Microsoft Exchange Unified Messaging Service に発行します。これによって、FAX メッセージのプロパティと、メールボックス サーバーによって作成された FAX メッセージのプロパティが一致するようにします。最後に、メールボックス サーバーが再度、最終 FAX メッセージを送信します。これには着信 FAX の電子メール メッセージと .tif 添付ファイルが含まれます。次に、MAPI RPC を使用して、完成した書式付きバージョンの FAX メッセージが意図した受信者のメールボックスを含むメールボックス サーバーに配信されます。

ページのトップへ

## FAX 呼び出しの参照方法

着信 FAX 呼び出しは、VoIP ゲートウェイまたは SIP ピア (メディア ゲートウェイ) からの SIP re-INVITE、SIP ピアによる CNG (呼び出し元の FAX トーン) 通知、またはメールボックス サーバーによる CNG 検出を介してメールボックス サーバーに通知できます。次のサブセクションで、それぞれのケースの FAX 呼び出し参照について詳しく説明します。

## SIP ピアからの Re-INVITE

UM パイロット番号に対する着信呼び出しが、UM にボイス (RTP/オーディオ) SDP プロファイルを使った INVITE として指定されます。

1.  UM が招待を受け入れ、メディア ストリームが確立されます。呼び出しが確立されると、発信者によって FAX 送信が開始されます。

2.  SIP ピアは、呼び出し元の FAX トーン (CNG) を検出します。SIP ピアがメールボックス サーバーに re-INVITE を発行します。今回は、SDP の FAX (T.38 または G.711) プロファイルを指定します。

3.  UM は、200 OK で招待に応答します。これにより、SIP ピアが "保留" になります。

4.  UM が REFER を発行し、SIP (CNG) ピアが、構成データから取得された FAX パートナー ソリューションのエンド ポイントを参照します。

5.  SIP ピアが FAX セッション INVITE を FAX パートナー ソリューションに送信します。

6.  FAX パートナー ソリューションが招待を受け入れ、SIP ピアとのメディア セッションが確立されます。

## SIP ピアによる CNG 通知

UM パイロット番号に対する着信呼び出しが、UM にボイス (RTP/オーディオ) SDP プロファイルを使った INVITE として指定されます。

1.  UM が招待を受け入れ、メディア ストリームが確立されます。呼び出しが確立されると、発信者によって FAX 送信が開始されます。

2.  SIP ピアが呼び出し元の FAX トーン (CNG) を検出します。SIP ピアは、RFC 4733 に準拠した RTP ストリームで CNG 通知を送信することで、UM サーバーに FAX を通知します。

3.  UM は、その通知に応答して、REFER を即座に発行し、SIP ピアが、構成データから取得された FAX パートナー ソリューションのエンド ポイントを参照します。

4.  SIP ピアが FAX セッション INVITE を FAX パートナー ソリューションに送信します。

5.  FAX パートナー ソリューションが招待を受け入れます。

6.  SIP ピアとのメディア セッションが確立されます。

## メールボックス サーバーによる CNG 検出

UM パイロット番号に対する着信呼び出しが、UM にボイス (RTP/オーディオ) SDP プロファイルを使った INVITE として指定されます。UM が招待を受け入れ、メディア ストリームが確立されます。

1.  呼び出しが確立されると、発信者によって FAX 送信が開始されます。

2.  メールボックス サーバーが RTP オーディオ ストリームで FAX トーン (CNG) を検出します。

3.  UM は、その通知に応答して、REFER を即座に発行し、SIP ピアが、構成データから取得された FAX パートナー ソリューションのエンド ポイントを参照します。

4.  SIP ピアが FAX セッション INVITE を FAX パートナー ソリューションに送信します。

5.  FAX パートナー ソリューションが招待を受け入れます。

6.  SIP ピアとのメディア セッションが確立されます。

ページのトップへ

## FAX 送受信の構成

既定では、メールボックス サーバーの役割をインストールすると、サーバーは、着信 FAX 呼び出しを処理したり、UM が有効なユーザーに配信したりできるように構成されません。UM を FAX パートナー サーバーと一緒に構成するには、UM メールボックス ポリシーを構成し、メールボックス サーバーと FAX パートナー サーバー間で認証を構成する必要があります。詳細については、「[着信 FAX の設定](setting-up-incoming-faxing-exchange-2013-help.md)」を参照してください。

ページのトップへ

## 電話番号と FAX 送受信

Exchange Unified Messaging では、FAX メッセージを受信するように UM が有効なユーザーを構成するときに、以下のオプションを使用できます。

  - FAX とボイス メールの両方に使用する個々のユーザーの DID (Direct Inward Dial) 電話番号。

  - FAX の受信に使用する各ユーザー用の個別の DID 電話番号。

  - すべてのFAX を受信する全ユーザー用の中央の FAX 電話番号。

## 単一の DID 電話番号

ユニファイド メッセージングの <strong>UM メールボックスを有効にする</strong> ページまたは **Enable-UMMailbox** コマンドレットを使用してユーザーのユニファイド メッセージングを有効にするときは、そのユーザーに少なくとも 1 つの内線番号を指定する必要があります。この内線番号はユーザーごとに有効にし、特定のダイヤル プラン内で一意である必要があります。この内線は、ユニファイド メッセージングで適切なユーザーを見つけるために使用され、またユーザーのメールボックスに音声メッセージと FAX メッセージを配信するために使用されます。詳細については、「[Enable-UMMailbox](https://technet.microsoft.com/ja-jp/library/aa998033\(v=exchg.150\))」をご覧ください。

単一の DID 番号により、FAX を構成して、ユーザーが単一の DID 番号を音声と FAX の両方に使用できるようにします。この構成は管理が容易で、余分な DID 番号を使用せずに済みます。FAX 呼び出しが到着したときにユーザーが不在の場合や電話中の場合は、UM が通話に応答し、FAX トーンを検出し、FAX メッセージを作成してユーザーに送信します。

FAX の送受信に単一の DID 電話番号を使用するユーザーが、不在ではないときまたは電話中に、FAX マシンから呼び出しを受けた場合、以下を実行できます。

  - 電話が鳴ったときに応答せず、FAX 呼び出しが転送されてメールボックス サーバーが応答し、FAX メッセージが作成されて自分のメールボックスに転送されるようにする。

  - FAX 呼び出しに応答し、それを自分に転送して、呼び出しが転送されてメールボックス サーバーが応答し、FAX メッセージが作成されて自分のメールボックスに転送されるようにする。

  - 発信者が FAX 送信を再試行するのを待ち、FAX 呼び出しがメールボックス サーバーに転送されるようにする。

このように、単一の DID 番号を使用する場合、ユーザーは FAX メッセージを受信するために追加の操作を行う必要があります。

ページのトップへ

## 複数の DID 電話番号

ユーザーのユニファイド メッセージングを有効にするときは、そのユーザー用に少なくとも 1 つの内線番号を入力する必要があります。Exchange 管理センター (EAC) を使用すると、UM が有効なユーザーに複数の内線番号を追加できます。詳細については、「[内線番号の追加](add-an-extension-number-exchange-2013-help.md)」を参照してください。

複数の内線番号の追加は、UM が有効なユーザーが次の状況にあるときに役立ちます。

  - 多くの FAX を受信する。

  - FAX を受信するために電話に応答したくない。

  - 電話に応答して FAX トーンを聞きたくない。

複数の内線の追加は単一の内線を使用する場合よりも複雑で、PBX または IP PBX 上で追加の構成設定が必要になる場合があります。UM が有効なユーザーに複数の内線番号を構成するには、使用可能であり、かつ組織で使用されていない DID 内線番号が必要です。組織で使用できる DID 内線番号の数が限られている場合は、UM が有効なユーザー用に複数の番号を使用することは適切ではありません。

複数の DID 内線番号を使用することの利点は、UM が有効なユーザーが 1 つの DID 内線番号で音声呼び出しを受信し、別の DID 内線番号で FAX 呼び出しを受信することです。ユーザーにとっては、音声呼び出しと FAX 呼び出しに個別の DID 番号を使用する方が簡単です。

特定のユーザーに 2 つの DID 内線番号を構成する場合、DID 内線番号は別々の UM ダイヤル プランに含まれている可能性があります。2 つの DID 番号を使用するには、ダイヤル プランを作成して、メールボックス サーバーを FAX 呼び出しを受信して FAX メッセージをユーザーに転送する専用サーバーとして使用します。詳細については、「[UM ダイヤル プランを作成する](create-a-um-dial-plan-exchange-2013-help.md)」を参照してください。

UM が有効なユーザーに複数の DID 内線番号を構成するときは、以下のオプションを使用できます。

  - **1 つの内線はユニファイド メッセージングなしの FAX 用、もう 1 つは音声用**   この種類の構成はユーザーごとに有効にし、使用できる余分な DID 内線番号や未使用の DID 内線番号がある場合に使用します。1 つの DID 内線番号はユーザーのボイス メール番号として公開し、もう 1 つの DID 内線番号はユーザーの FAX 番号として公開します。ユーザーが電話に応答しない、またはビジー信号で応答された音声呼び出しは、メールボックス サーバーに転送され、音声メッセージが作成されて UM が有効なユーザーのメールボックスに送信されます。もう 1 つの内線番号は、FAX マシンまたは FAX モデムがインストールされている別のコンピューターに接続できます。この構成では、メールボックス サーバーは FAX 呼び出しを処理せず、FAX メッセージは UM が有効なユーザーのメールボックスに送信されません。

  - **1 つの内線番号は FAX 用、もう 1 つは音声用**   この種類の構成はユーザーごとに有効にし、組織で使用できる DID 内線番号が多数ある場合に使用できます。この構成ではどちらの DID 内線番号への呼び出しも、応答がない場合またはビジー信号で応答された場合はメールボックス サーバーに転送され、呼び出される DID 内線番号に応じてメールボックス サーバーで音声メッセージまたは FAX メッセージが作成されます。ユーザーは 1 つの番号を音声用に、もう 1 つを FAX 用に公開しますが、メールボックス サーバーは、DID 内線番号で受信した呼び出しの種類を検出し、どちらの DID 内線番号への呼び出しからでも音声メッセージまたは FAX メッセージを作成できます。これは、ユーザーが別の FAX マシンまたは着信 FAX 呼び出しに応答するための FAX モデムがインストールされている専用コンピューターを持っていない場合に、非常に役に立ちます。

  - **1 つは FAX 用の "実体のない" 内線、もう 1 つは音声用**   この種類の構成は、ユーザーごとに有効にします。基本的には、2 つの DID 番号 (1 つは FAX 用、もう 1 つは音声用) を使用する構成と同じです。ただしこの構成では、UM が有効なユーザーの FAX 呼び出し用として公開される番号は、PBX で "実体のない" 内線として構成されます。この "実体のない" DID 内線番号で受信される着信呼び出しは、常にメールボックス サーバーに転送されます。
    
    この種類の構成の利点は、着信 FAX 呼び出しがメールボックス サーバーによって応答されることです。電話に応答がない場合はメールボックス サーバーによって FAX が作成され、ユーザーの邪魔をすることなく UM が有効なユーザーのメールボックスに転送されます。ユーザーの邪魔をすることなく自動で転送されるのは、ユーザーの近くに電話や FAX デバイスが配置されておらず、ユーザーには着信呼び出しの呼び出し音が聞こえないためです。
    
    この種類の構成の不利な点は、使用できる追加の DID 内線が必要であることと、呼び出しをメールボックス サーバーに転送するように PBX または IP PBX を構成する必要があることです。

## 中央の FAX 電話番号

ユニファイド メッセージングの <strong>UM メールボックスを有効にする</strong> ページまたは **Enable-UMMailbox** コマンドレットを使用してユーザーのユニファイド メッセージングを有効にするときは、そのユーザーに少なくとも 1 つの内線番号を指定する必要があります。ただし、中央の FAX 番号を受信 FAX 用に構成する必要がある場合は、すべての FAX 受信に使用する別の UM が有効なメールボックスをセットアップする必要があります。

一部の組織、特に毎日多くの FAX を受信する組織では、組織全体で 1 つの FAX 番号を公開する場合があります。組織内のユーザーに FAX を送信するすべての発信者がこの FAX 番号を使用します。

組織全体用に 1 つの FAX 番号を公開すると、ユーザーが受信する FAX の種類を組織で管理できます。この構成の利点は、単一の DID 内線番号または外線電話番号のみあればよいということです。また、UM が有効なユーザーごとに FAX 用の DID 番号を指定する必要がありません。ただし、FAX の送付状や FAX 自体に含まれている情報を基に着信 FAX を組織内のユーザーに配布する、"FAX 担当秘書" のような人が必要になります。


> [!NOTE]
> Exchange Unified Messaging で、光学式文字認識 (OCR) と共に中央の FAX 番号を使用することはできません。この種類の構成では、中央の FAX 番号を使用することができます。ただし、人が受信者に FAX を配布するのではなく、FAX ソフトウェアが FAX を受信し、OCR を実行し、送付状や FAX メッセージの情報に基づいて受信者を見つけます。



組織全体で単一の FAX 番号を使用することは、次のような状況で便利です。

  - 組織内のユーザーがメールボックスで受信する FAX 数が多すぎて効果的に管理できない。

  - ユーザーがメールボックスで受信するスパム FAX の数が多すぎる。

  - ビジネス ニーズが複雑すぎるため、受信 FAX を受け入れて目的のメールボックスに転送するトランスポート ルールの作成を保証できない。この状況は、たとえば組織がユーザーに、特定の FAX を 1 つのグループにルーティングし、他の FAX を別のグループにルーティングすることを要求する場合に現実的ではない可能性があります。詳細については、「[メール フローやトランスポート ルール](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)」を参照してください。

  - Outlook を使用した FAX メッセージのフィルター処理が効果的でない。

ページのトップへ

## UM FAX メッセージのジャーナリング

ジャーナリングを実装する組織の多くでは、ユニファイド メッセージングを使用して、電子メール、ボイス メール、および FAX のインフラストラクチャを統合している場合もあります。ただし、ユニファイド メッセージングにより生成されたメッセージのジャーナル レポートをジャーナリング プロセスで処理したくはない場合もあるでしょう。この場合、メールボックス サーバーによって処理されるボイス メール メッセージや不在着信通知メッセージのジャーナリングを実行するか、あるいはそのようなメッセージをスキップするかを決めることができます。組織でボイス メールや不在着信通知のジャーナリングが不要な場合は、メッセージをスキップすることで、ジャーナル レポートを格納するために必要なハード ディスク領域を減らすことができます。ボイス メール メッセージや不在着信通知メッセージのジャーナリングを有効または無効にすると、その変更は組織内のすべてのトランスポート サーバーに適用されます。詳細については、「[ジャーナル](journaling-exchange-2013-help.md)」を参照してください。


> [!NOTE]
> ユニファイド メッセージング ボイス メールや不在着信通知メッセージをジャーナルの対象にしないというジャーナル ルールを構成している場合でも、メールボックス サーバーで生成された FAX を含むメッセージは常にジャーナルの対象になります。



ページのトップへ

