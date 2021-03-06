﻿---
title: 'Outlook の保護ルール: Exchange 2013 Help'
TOCTitle: Outlook の保護ルール
ms:assetid: bd7d0ad7-1f8e-46da-a74b-58c58f3eff93
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dd638178(v=EXCHG.150)
ms:contentKeyID: 49896446
ms.date: 04/24/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Outlook の保護ルール

 

_**適用先:** Exchange Server 2013_

_**トピックの最終更新日:** 2016-12-09_

情報作業者は毎日、電子メールで機密情報をやり取りしています。これには財務報告書や財務データ、顧客や従業員の情報、機密製品情報や仕様などが含まれます。Microsoft Exchange Server 2013、Microsoft Outlook、および Microsoft OfficeOutlook Web App では、ユーザーは Active Directory Rights Management サービス (AD RMS) 権利ポリシー テンプレートを適用することで、Information Rights Management (IRM) 保護をメッセージに適用できます。これには、組織内で AD RMS を展開することが必要です。AD RMS の詳細については、「[Active Directory Rights Management サービス](https://go.microsoft.com/fwlink/p/?linkid=129823)」を参照してください。

ただし、ユーザーの指示に任された場合、メッセージは IRM 保護なしで、クリア テキストで送信される可能性があります。ホストされたサービスとして電子メールを使用する組織の場合、メッセージがクライアントから送信されて、組織の境界外にルーティングおよび保存される際、情報漏洩のリスクが生じます。電子メールをホストする企業に明確な手順があり、情報漏洩のリスクを軽減できるようにチェックしても、メッセージが組織の境界から出ると、組織は情報を制御できなくなります。Outlook の保護ルールは、この種の情報漏洩の保護に役立ちます。

IRM 管理に関連する管理タスクについては、「[Information Rights Management の手順](information-rights-management-procedures-exchange-2013-help.md)」を参照してください。

## Outlook の自動 IRM 保護

Exchange 2013 では、Outlook 保護ルールは、IRM 保護を Exchange 2013 のメッセージに自動的に割り当てることにより、情報漏洩のリスクから組織を保護します。メッセージは Outlook クライアントを出る前に IRM で保護されます。この保護機能は、ポートされるファイル形式を使用するすべての添付ファイルにも適用されます。

Outlook 保護ルールを Exchange 2013 サーバー上に作成すると、ルールは Exchange Web サービスの使用により、自動的に Outlook 2010 に配布されます。Outlook 2010 でルールを適用するには、指定する AD RMS 権利ポリシー テンプレートがユーザーのコンピューターで使用できる必要があります。


> [!IMPORTANT]
> 権利ポリシー テンプレートを AD RMS サーバーから削除した場合、削除されたテンプレートを使用するすべての Outlook 保護ルールを変更する必要があります。Outlook 保護ルールで、削除された権利ポリシー テンプレートが継続使用され、トランスポート復号化が組織内で有効化されている場合、復号化エージェントは、使用できなくなったテンプレートで保護されたメッセージを解読できなくなります。トランスポート復号化が必須として構成されている場合、トランスポート サービスはメッセージを拒否し、配信不能レポート (NDR) を送信者に送信します。トランスポート復号化の詳細については、「<A href="transport-decryption-exchange-2013-help.md">トランスポート復号化</A>」を参照してください。AD&nbsp;RMS 権利ポリシー テンプレートの詳細については、「<A href="https://go.microsoft.com/fwlink/p/?linkid=179455">AD RMS ポリシー テンプレートに関する考慮事項</A>」を参照してください。<BR>Windows Server 2008 以降では、権利ポリシー テンプレートは削除する代わりにアーカイブすることができます。アーカイブされたテンプレートは引き続き、コンテンツにライセンスするために使用できますが、Outlook 保護ルールを作成または変更するときに、アーカイブされたテンプレートは、テンプレート一覧に含まれません。



Outlook 保護ルールはトランスポート保護ルールに似ています。両方ともメッセージの条件に基づいて適用され、AD RMS 権利保護テンプレートを適用してメッセージを保護します。ただし、メールボックス サーバー上のトランスポート サービスには、トランスポート ルール エージェントによってトランスポート保護ルールが適用されます。Outlook 2010 では、メッセージがユーザーのコンピューターから送信される前に Outlook 保護ルールが適用されます。Outlook 保護ルールによって保護されたメッセージは、IRM 保護が既に適用された状態でトランスポート パイプラインに入ります。また、Outlook 保護ルールで保護されたメッセージは、送信者のメールボックスの送信済みアイテム フォルダーに、暗号化された形式で保存されます。


> [!NOTE]
> トランスポート復号化が Exchange 組織で有効化されている場合、組織の AD RMS サーバーを使用することで、Outlook 保護ルールで IRM 保護されているメッセージは、トランスポート サービス上の復号化エージェントによって解読できます。メッセージ コンテンツは、トランスポート ルール エージェントおよびトランスポート サービスにインストールされた他のトランスポート エージェントによって検査することができます。トランスポート復号化の詳細については、「<A href="transport-decryption-exchange-2013-help.md">トランスポート復号化</A>」を参照してください。



トランスポート保護ルールを使用する場合、メッセージがトランスポート サービスで自動的に保護されるかどうかはユーザーにはわかりません。Outlook 保護ルールを Outlook 2010 内のメッセージに適用する場合、ユーザーはメッセージが IRM 保護されるかどうかがわかります。必要に応じて、ユーザーは他の権利ポリシー テンプレートを選択することもできます。

## Outlook の保護ルールの作成

Outlook 保護ルールを作成するには、Exchange 管理シェルで [New-OutlookProtectionRule](https://technet.microsoft.com/ja-jp/library/dd298182\(v=exchg.150\)) コマンドレットを使用する必要があります。詳細な手順については、「[Outlook 保護ルールを作成する](create-an-outlook-protection-rule-exchange-2013-help.md)」を参照してください。

ルールを作成する際、ユーザーが IRM 保護を削除するか、またはルールで指定されているものとは異なる AD RMS 権利ポリシー テンプレートを適用することで、ルールを上書きできるかどうかを指定できます。ユーザーが Outlook 保護ルールによって適用された IRM 保護を上書きする場合は、Outlook 2010 によってメッセージに `X-MS-Outlook-Client-Rule-Overridden` ヘッダーが挿入されるため、ルールがユーザーによって上書きされたかどうかを判断することができます。

## Outlook 保護ルールの述語

Outlook 保護ルールにより、IRM 保護を自動的に Outlook 2010 に適用するための 3 つの述語を使用できます。

  - **FromDepartment**   *FromDepartment* 述語は、送信者の部署属性を Active Directory 内で検索し、送信者の部署がルールで指定された部署に一致する場合は、メッセージを自動的に IRM 保護します。たとえば、調査部署によって送信されたすべてのメッセージを自動的に保護するための Outlook 保護ルールを作成できます。

  - **SentTo**   組織では、All Company 配布グループまたは Finance 配布グループなど、機密情報を扱う特定の受信者に送信されたメッセージの保護の必要がある場合があります。*SentTo* 述語を使用すると、指定の受信者に送信されたメッセージを自動的に IRM 保護するための Outlook 保護ルールを作成することができます。

  - **SentToScope**   *SentToScope* 述語を使用すると、組織の内部または外部に送信されたメッセージを自動的に IRM 保護するための Outlook 保護ルールを作成することができます。たとえば、*SentToScope* 述語を *FromDepartment* 述語と共に使用すると、特定の部署から内部ユーザーに送信されたメッセージを IRM 保護することができます。

