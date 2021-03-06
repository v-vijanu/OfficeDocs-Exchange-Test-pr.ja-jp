﻿---
title: 'Outlook for iOS および Android for Exchange Server のパスワードとセキュリティ'
TOCTitle: Passwords and Security in Outlook for iOS and Android for Exchange Server
ms:assetid: e5565beb-7ef3-47c4-8daf-6d8f1d22dceb
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Mt465750(v=EXCHG.150)
ms:contentKeyID: 70090795
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Passwords and Security in Outlook for iOS and Android for Exchange Server

 

_**適用先:** Exchange Server 2010, Exchange Server 2013_

_**トピックの最終更新日:** 2018-04-01_

**概要**:この記事では、Exchange Server を使った iOS および Android 用の Outlook でパスワードとセキュリティがどのように機能するかについて取り上げます。

iOS および Android 用の Outlook アプリを初めて Exchange のオンプレミス環境で実行すると、Outlook がランダムな AES-128 キーを生成します。このキーは、*デバイス キー*と呼ばれ、ユーザーのデバイスにのみ格納されます。

## アカウントの作成とパスワードの保護

ユーザーが Exchange にログオンすると、ユーザー名、パスワード、一意の AES-128 デバイス キーがユーザーのデバイスから TLS 接続を介して Outlook サービスに送信されます。デバイス キーは実行時の計算メモリ内に保持されます。Exchange サーバーでパスワードを検証した後、Outlook サービスではデバイス キーを使ってパスワードが暗号化され、暗号化されたパスワードはサービスに格納されます。その間に、デバイス キーはメモリから消去され、Outlook サービスに格納されることはありません (キーはユーザーのデバイスにのみ格納されます)。

次に、ユーザーが Exchange に接続してメールボックス データを取得しようとすると、TLS でセキュリティ保護された接続を介してデバイス キーが再度デバイスから Outlook サービスに渡されます。デバイス キーは、実行時の計算メモリ内のパスワードを復号化するのに使用されます。復号化されると、パスワードはサービスに格納されることも、ローカル ストレージ ディスクに書き込まれることもなく、デバイス キーは再度メモリから消去されます。

Outlook サービスの実行時にパスワードが復号化されると、サービスは Exchange サーバーに接続でき、メール、予定表、その他のメールボックス データを同期できます。ユーザーが定期的に Outlook を開き使用し続ける限り、Outlook サービスは、ユーザーの復号化されたパスワードのコピーをメモリ内に維持し、Exchange サーバーへの接続をアクティブに保ちます。

## アカウントの非アクティブ状態とメモリからのパスワードのフラッシュ

非アクティブ状態が 3 日続くと、Outlook サービスは復号化されたパスワードをメモリからフラッシュします。復号化されたパスワードがフラッシュされると、Outlook サービスではユーザーのメールボックスにアクセスできなくなります。暗号化されたパスワードは引き続き Outlook サービスに保管されますが、デバイス キーがないと再度復号化することはできません。デバイス キーはユーザーのデバイスからのみ利用できます。

ユーザー アカウントは次の 3 つの場合に非アクティブになります。

  - iOS および Android 用の Outlook がユーザーによってアンインストールされる。

  - \[設定\] オプションでアプリのバックグラウンド更新が無効にされた後、Outlook が強制終了される。

  - デバイスにインターネット接続がないため、Outlook が Exchange と同期できない。


> [!NOTE]
> 単純にユーザーがアプリを一定の期間 (週末または休暇の間) 開かないために、Outlook が非アクティブになることはありません。アプリのバックグラウンド更新が有効にされている限り (iOS および Android 用の Outlook の既定の設定)、プッシュ通知や電子メールのバックグラウンド同期などの機能はアクティビティの一部として認識されます。



**暗号化されたパスワードやメッセージ キャッシュをハード ディスクからフラッシュする**

Outlook サービスは、非アクティブなアカウントを週単位のスケジュールでフラッシュ (削除) します。ユーザー アカウントが非アクティブになると、Outlook サービスは、暗号化されたパスワードとユーザーのすべてのキャッシュされたメールボックス コンテンツの両方をサービスからフラッシュします。

**デバイスとサービスのセキュリティの組み合わせ**

各ユーザーの一意のデバイス キーが Outlook サービスに保存されることはなく、ユーザーの Exchange パスワードがデバイスに保存されることもありません。このアーキテクチャは、悪意のある人がユーザーのパスワードにアクセスするには、Outlook サービスへの未承認のアクセスとユーザーのデバイスへの物理アクセスが必要であることを意味します。

組織内のデバイスで PIN ポリシーと暗号化を有効にすると、悪意のある人もデバイス キーにアクセスするためだけにデバイスの暗号化を解除しなければならなくなります。これらはすべて、デバイスが侵害されており、デバイスに対してリモート ワイプを要求できることにユーザーが気付く前に行われる必要があります。

## パスワード セキュリティに関する FAQ

iOS および Android 用の Outlook のセキュリティ設計と設定に関してよく寄せられる質問を以下に示します。

## Outlook の Exchange Server へのアクセスをブロックすると、ユーザーの資格情報は Outlook サービスに保存されますか。

iOS および Android 用の Outlook がオンプレミスの Exchange サーバーにアクセスできないようにした場合、最初の接続は Exchange によって拒否されます。ユーザーの資格情報は Outlook サービスには保存されず、失敗した接続の試行時に表示された資格情報はメモリからすぐにフラッシュされます。

## Outlook サービスへの転送時に一意のデバイス キーとユーザーのパスワードはどのように暗号化されますか。

Outlook アプリと Outlook サービス間のすべての通信は暗号化された TLS 接続によって行われます。iOS および Android 用の Outlook は、Outlook サービスでのみ接続でき、それ以外では接続できません。

## Outlook サービスからユーザーの資格情報とメールボックス情報を削除する方法を教えてください。

Outlook のサービスから情報を削除するのには 3 つの方法があります。

  - オプション 1:Exchange に接続するためにアプリを使用したことのある各ユーザーにリモート ワイプを開始します。

  - オプション 2:すべてのユーザーに iOS および Android 用の Outlook を削除してもらいます。すべてのデータは約 3 ～ 7 日後に Outlook サービスから削除されます。

  - オプション 3:ユーザーに、Outlook アプリから各自のアカウントを削除し、さらに各自のデバイスからアプリを削除してもらいます。アプリで、ユーザーに <strong>設定</strong> に移動してもらい、<strong>アカウント設定</strong>、<strong>アカウントの選択</strong>、<strong>アカウントの削除</strong> の順にタップしてもらいます。

## アプリは閉じられたかアンインストールされているのに、Exchange サーバーに接続されているようです。これが生じているのはなぜですか。

Outlook サービスは実行時の計算メモリにあるユーザー パスワードを復号化してから、復号化されたパスワードを使って Exchange に接続します。Outlook サービスは、メールボックス データをフェッチおよびキャッシュするためにデバイスに代わって Exchange に接続されるため、Outlook がデータを要求しなくなったことをサービスが検知するまで、短い期間接続が続く場合があります。

ユーザーが最初に <strong>アカウントの削除</strong> オプションを使用せずにデバイスからアプリをアンインストールすると、上記の「アカウントの非アクティブ状態とメモリからのパスワードのフラッシュ」で説明されているように、Outlook サービスはアカウントが非アクティブになるまで Exchange サーバーに接続され続けます。このアクティビティを停止するには、上記の FAQ のオプション 1 またはオプション 3 に従うか、「[iOS および Android 用の Outlook のブロック](https://technet.microsoft.com/ja-jp/library/mt759239\(v=exchg.150\))」で説明されているようにアプリをブロックします。

## ユーザー パスワードは、他の Exchange ActiveSync クライアントを使用する場合より、iOS および Android 用の Outlook で使用する方が安全性は低いですか。

いいえ。EAS クライアントでは通常、ユーザーのデバイスでローカルにユーザーの資格情報が保存されます。つまり、盗難または侵害されたデバイスを通して、悪意のある人物によってユーザーのパスワードにアクセスされる可能性があります。iOS および Android 用の Outlook のセキュリティ設計により、悪意のある人物には、Outlook クラウド サービスへの未承認のアクセス**および**ユーザーのデバイスへの物理アクセスが必要です。

## Outlook サービスからデータが削除された後に、ユーザーが iOS および Android 用の Outlook を使用しようとするとどうなりますか。

(デバイスでアプリのバックグラウンド更新を無効にしたり、デバイスをインターネットから一定の時間切断したりすることにより) ユーザー アカウントが非アクティブになると、Outlook アプリはアプリが次に起動されるときに Outlook サービスに再接続され、パスワードの暗号化と電子メールのキャッシュ処理が再開されます。これらはどれも、ユーザーには表示されません。

## 一時的にキャッシュされたメールボックス データは、Outlook サービスに格納されている間、どのようにセキュリティで保護されるのでしょうか。

[Azure のセキュリティ センター](https://azure.microsoft.com/support/trust-center/)で、データを保護する現在の詳細を参照できます。前に述べたように移行 Azure から Office 365 にします。これらのサービスのセキュリティは、 [Office 365 の信頼の中心](https://go.microsoft.com/fwlink/p/?linkid=525776)に記載されています。

