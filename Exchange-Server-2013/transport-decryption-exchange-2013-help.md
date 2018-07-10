﻿---
title: 'トランスポート復号化: Exchange 2013 Help'
TOCTitle: トランスポート復号化
ms:assetid: 4267c46d-f488-404d-a5cb-51f9127461c0
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd638122(v=EXCHG.150)
ms:contentKeyID: 49896221
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# トランスポート復号化

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2015-04-07_

Microsoft Exchange Server 2013、Microsoft Outlook 2010 以降、および Microsoft Office Outlook Web App では、ユーザーは Information Rights Management (IRM) を使用して自分のメッセージを保護できます。Outlook 2010 クライアントからメッセージが送信される前に、IRM 保護をメッセージに自動的に適用する Outlook 保護ルールを作成できます。また、ルール条件に一致する送信中のメッセージに IRM 保護が適用されるように、トランスポート保護ルールを作成することもできます。トランスポート復号化を使用すると、IRM で保護されたメッセージング コンテンツにアクセスして、メッセージング ポリシーを強制できます。

IRM の管理に関連する管理タスクについては、「[Information Rights Management の手順](information-rights-management-procedures-exchange-2013-help.md)」を参照してください。

## 他の暗号化ソリューションの制限

ビジネスへの影響が大きい (HBI) 情報および個人識別情報 (PII) を含む機密情報を保護することは組織にとって重要であり、電子メールのメッセージと添付ファイルの暗号化を考慮します。S/MIME のような電子メールの暗号化ソリューションは、昔から利用可能でした。これらの暗号化ソリューションは、さまざまな種類の組織に採用され、さまざまなレベルで見受けられました。ただし、このようなソリューションは次の課題を提示します。

  - **メッセージング ポリシーを提供することが不可能**   組織はまた、メッセージング ポリシーに従っていることを確認するためにメッセージング コンテンツの検査を必要とする、法令遵守の要件にも直面しています。ただし、S/MIME を含む、ほとんどのクライアント ベースの暗号化ソリューションによって暗号化されたメッセージは、サーバー上でコンテンツを検査できません。コンテンツの検査ができないと、すべてのメッセージがメッセージング ポリシーに準拠したユーザーによって送信または受信されたことを、組織は検証できません。たとえば、法的規則に従うために、社会保障番号などの PII を検出して自動的にメッセージに免責事項を適用するようトランスポート ルールを構成しました。メッセージが暗号化されている場合、トランスポート サービスのトランスポート ルール エージェントはメッセージのコンテンツにアクセスできず、そのため免責事項を適用できません。この結果、ポリシーの違反になります。

  - **セキュリティの低下**   ウイルス対策ソフトウェアは暗号化されたメッセージ コンテンツをスキャンできないので、ウイルスやワームなどの悪意のあるコンテンツのリスクに組織をさらすことになります。暗号化されたメッセージはほとんどのユーザーによって信頼されたものと一般的にみなされますので、組織全体にウイルスを蔓延させる可能性が増加します。たとえば、"全従業員" 配布リストに送信されるすべてのメッセージに対して自動的に、Company Confidential Rights Management Service (RMS) テンプレートを使用して IRM 保護を適用するよう Outlook 保護ルールを構成しました。ユーザーのワークステーションは、\[全員へ返信\] を自動的に使用してメッセージに返信することで広がるウイルスに感染しました。ウイルスを運んでいるメッセージが暗号化されている場合、ウイルス対策ソフトのスキャナーはメッセージをスキャンできません。

  - **カスタムのトランスポート エージェントへの影響**   多くの組織では、規制遵守、セキュリティ、またはカスタムのメッセージ ルーティングに対する追加の処理要件を満たすためなどの、さまざまな目的のためにカスタムのトランスポート エージェントを開発しています。組織によって開発された、メッセージを検査または変更するカスタムのトランスポート エージェントは、暗号化されたメッセージを処理出来ません。組織で開発したカスタムのトランスポート エージェントがメッセージ コンテンツにアクセスできない場合、メッセージの暗号化によって、カスタムのトランスポート エージェントが開発された目標を組織が達成するのを阻害している可能性があります。

## 暗号化されたコンテンツにトランスポート復号化を使用する

Exchange 2013 では、IRM 機能がこれらの問題に対処します。メッセージが IRM で保護されている場合、トランスポート復号化を使用するとメッセージを送信中に復号化できます。IRM で保護されたメッセージは、コンプライアンスのためのトランスポート エージェントである復号化エージェントによって復号化されます。


> [!NOTE]
> Exchange 2013 では、復号化エージェントはビルトイン エージェントです。ビルトイン エージェントは、<STRONG>Get-TransportAgent</STRONG> コマンドレットによって返されるエージェントの一覧には含まれていません。詳細については、「<A href="transport-agents-exchange-2013-help.md">トランスポート エージェント</A>」を参照してください。



復号化エージェントは、次の種類の IRM で保護されたメッセージを復号化します。

  - Outlook Web App でユーザーによって IRM で保護されたメッセージ。

  - Outlook 2010 でユーザーによって IRM で保護されたメッセージ。

  - Exchange 2013 および Outlook 2010 の Outlook 保護ルールで、自動的に IRM で保護されたメッセージ。


> [!IMPORTANT]
> 組織の AD&nbsp;RMS サーバーによって IRM 保護されたメッセージだけが、復号化エージェントによって復号化されます。




> [!NOTE]
> トランスポート保護ルールを使用して、送信中保護されたメッセージは、復号化エージェントによって復号化される必要はありません。復号化エージェントは、<STRONG>OnEndOfData</STRONG> および <STRONG>OnSubmit</STRONG> トランスポート イベントで実行されます。トランスポート保護ルールはトランスポート ルール エージェントによって適用され、<STRONG>OnRoutedMessage</STRONG> イベントを発生させます。IRM 保護は <STRONG>OnRoutedMessage</STRONG> イベントの暗号化エージェントによって適用されます。トランスポート エージェント、およびそれらが登録される SMTP イベントの一覧の詳細については、<A href="transport-agents-exchange-2013-help.md">トランスポート エージェント</A> を参照してください。



トランスポート復号化は、Active Directory フォレストでメッセージを処理する、最初の Exchange 2013 トランスポート サービスで実行されます。メッセージが別の Active Directory フォレストのトランスポート サービスに転送される場合、メッセージは再び復号化されます。復号化の後は、暗号化されていないコンテンツはサーバー上の他のトランスポート エージェントで利用可能です。たとえば、トランスポート サービスのトランスポート ルール エージェントは、メッセージ コンテンツを検索してトランスポート ルールを適用できます。免責事項の適用またはその他の方法によるメッセージの変更など、このルールで指定されたすべての操作は、暗号化されていないメッセージで行われます。ウイルス対策スキャナーなどの、サード パーティのトランスポート エージェントは、ウイルスとマルウェアについてメッセージをスキャンできます。他のトランスポート エージェントがメッセージを検査およびもしくはそれに変更を加えた後、復号化エージェントによって復号化される前と同じユーザー権限で再び暗号化されます。同じメッセージは、組織の他のメールボックス サーバー上の他のトランスポート サービスによって再び復号化されません。

復号化エージェントによって復号化されたメッセージは、再び暗号化されることなしにトランスポート サービスから出て行くことはありません。メッセージを復号化または暗号化しているときに一時的なエラーが返される場合、トランスポート サービスは操作を 2 度再試行します。3 回の失敗の後、エラーは永続的なエラーとして扱われます。再試行後に一時的なエラーが永続的なエラーとして扱われる場合を含めて、永続的なエラーが発生すると、トランスポート サービスはそれらを以下のように扱います。

  - 復号化中に永続的なエラーが発生すると、トランスポート復号化が `Mandatory` に設定されている場合にのみ配信不能レポート (NDR) が送信され、暗号化されたメッセージが NDR と共に送信されます。トランスポート復号化で利用可能な構成オプションの詳細については、後の「トランスポート復号化の構成」を参照してください。

  - 再暗号化中に永続的エラーが発生すると、NDR は常に復号化されたメッセージなしに送信されます。


> [!IMPORTANT]
> トランスポート サービスにインストールされた、すべてのカスタムまたはサード パーティのエージェントは、復号化されたメッセージにアクセスできます。このようなトランスポート エージェントの動作を考慮する必要があります。すべてのカスタムおよびサードパーティのトランスポート エージェントを、運用環境で展開する前に徹底的にテストすることをおすすめします。<BR>メッセージが復号化エージェントによって復号化された後に、トランスポート エージェントが新しいメッセージを作成し、その新しいメッセージに元のメッセージを埋め込む (添付する) 場合、新しいメッセージだけが保護されます。元のメッセージは、新しいメッセージの添付となり、再暗号化はされません。そのようなメッセージを受信する受信者は、添付されたメッセージを開いて、転送または返信などの操作を実行して、権限の適用をバイパスできます。



## トランスポート復号化の構成

トランスポート復号化は、Exchange 管理シェルの [Set-IRMConfiguration](https://technet.microsoft.com/ja-jp/library/dd979792\(v=exchg.150\)) コマンドレットを使用して構成します。ただし、トランスポート復号化を構成する前に、Exchange 2013 サーバーに、AD RMS サーバーによって保護されたコンテンツを復号化する権限を付与する必要があります。これを行うには、組織の AD RMS クラスター上に構成されたスーパー ユーザー グループにフェデレーション メールボックスを追加します。


> [!IMPORTANT]
> 各フォレストに AD&nbsp;RMS クラスターが展開されたクロス フォレスト AD&nbsp;RMS 展開では、フェデレーション メールボックスを各フォレストの AD&nbsp;RMS クラスター上のスーパー ユーザー グループに追加して、各 AD&nbsp;RMS クラスターに対して保護されたメッセージを Exchange 2013 メールボックス サーバーまたは Exchange 2010 ハブ トランスポート サーバー上のトランスポート サービスが復号化できるようにします。



詳細については、「[フェデレーション メールボックスを AD RMS のスーパー ユーザー グループに追加する](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md)」を参照してください。

Exchange 2013 では、トランスポート復号化を有効にするときに、2 つの異なる設定を使用できます。

  - **必須**   トランスポート復号化が `Mandatory` に設定されている場合、メッセージの復号化中に永続的なエラーが返されると、復号化エージェントはメッセージを拒否して NDR を送信者に返します。メッセージが正常に復号化できず、ウイルス対策スキャンおよびトランスポート ルールのような操作が適用できない場合に、組織がメッセージを配信したくない場合はこの設定を選択する必要があります。

  - **任意**   トランスポート復号化が "任意" に設定されると、復号化エージェントはベストエフォート アプローチを使用します。復号化できるメッセージは復号化されますが、復号化で永続的エラーが発生するメッセージもまた配信されます。組織がメッセージング ポリシーよりもメッセージの配信に重点を置いている場合は、この設定を使用する必要があります。

トランスポート復号化の構成の詳細については、「[トランスポート解読を有効または無効にする](enable-or-disable-transport-decryption-exchange-2013-help.md)」を参照してください。
