﻿---
title: 'UM ダイヤル プランを作成する: Exchange Online Help'
TOCTitle: UM ダイヤル プランを作成する
ms:assetid: 963ff2e1-515d-439a-953a-664174e5e283
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb123819(v=EXCHG.150)
ms:contentKeyID: 49896379
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.CreateUMDialPlanWizardForm.CreateUMDialPlanWizardPage
ms.translationtype: HT
---

# UM ダイヤル プランを作成する

 

_**適用先:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

ユニファイド メッセージング (UM) ダイヤル プランには、テレフォニー ネットワークに関連する構成情報が含まれています。UM ダイヤル プランによって、ボイス メールが有効なユーザーの内線電話番号からメールボックスへのリンクが確立されます。UM ダイヤル プランを作成するときに、内線番号の桁数、URI (Uniform Resource Identifier) タイプ、およびダイヤル プランの VoIP (Voice over IP) セキュリティ設定を構成できます。

UM ダイヤル プランを作成するたびに、UM メールボックス ポリシーも作成されます。UM メールボックス ポリシーには、"\<*ダイヤル プラン名*\> の既定のポリシー" という名前が付けられます。

UM ダイヤル プランに関連するその他の管理タスクについては、「[UM ダイヤル プラン手順](um-dial-plan-procedures-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 3 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[ユニファイド メッセージングのアクセス許可](unified-messaging-permissions-exchange-2013-help.md)」の「UM ダイヤル プラン」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## EAC を使用して UM ダイヤル プランを作成する

1.  
    
    EAC で、<strong>ユニファイド メッセージング</strong> \> <strong>UM ダイヤル プラン</strong> の順に選択し、<strong>新規</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックします。

2.  <strong>UM ダイヤル プランの新規作成</strong> ページで、次のボックスを入力します。
    
      - <strong>名前</strong>   ダイヤル プランの名前を入力します。一意な UM ダイヤル プラン名を必ず指定する必要があります。ただし、EAC およびシェルに表示するためにのみ使用されます。ダイヤル プランを作成した後で表示名を変更する必要が生じた場合は、最初に既存の UM ダイヤル プランを削除してから、適切な名前を持つ別のダイヤル プランを作成する必要があります。組織で複数の UM ダイヤル プランを使用している場合は、それぞれに意味のあるわかりやすい名前を使用することをお勧めします。UM ダイヤル プラン名の長さは 64 文字以下で、スペースを含めることができます。ただし、次の文字を含めることはできません。" / \\ \[ \] : ; | = , + \* ? \< \>.
        
        新しい UM ダイヤル プランには空白を含んだ名前を付けることができますが、ユニファイド メッセージングを Office Communications Server 2007 R2 または Microsoft Lync Server と統合する場合は、ダイヤル プランの名前に空白を含めることはできません。したがって、表示名に空白を含めてダイヤル プランを作成し、その後 Office Communications Server 2007 R2 または Lync Server と統合する場合は、まずそのダイヤル プランを削除してから、表示名に空白を含まない別のダイヤル プランを作成する必要があります。
        

        > [!IMPORTANT]
        > ダイヤル プラン名のボックスには 64 文字まで入力できますが、49 文字を超えるダイヤル プラン名は設定できません。49 文字を超えるダイヤル プラン名を作成しようとすると、エラー メッセージが表示されます。メッセージには、UM ダイヤル プラン名が長すぎるため、UM メールボックス ポリシーを生成できなかったことが表示されます。これは前述したように、ダイヤル プランを作成するときに、「<EM>&lt;ダイヤル プラン名&gt;</EM> Default Policy」という既定の UM メールボックス ポリシーも作成されるためです。Default Policy という 15 文字をダイヤル計画名に追加すると、文字の合計数は上限を超過します。UM ダイヤル プランと UM メールボックス ポリシー両方の <EM>name</EM> パラメーターは、いずれも最大 64 文字に設定できます。ただし、ダイヤル プラン名が 49 文字を超える場合、既定の UM メールボックス ポリシー名が 64 文字よりも長くなります。これはシステムでは許可されません。

    
      - <strong>内線番号の長さ (桁数)</strong>   ダイヤル プランの桁数を入力します。内線番号の桁数は、構内交換機 (PBX) または IP PBX で作成されるテレフォニー ダイヤル プランに基づきます。たとえば、テレフォニー ダイヤル プランに関連付けられているユーザーが、同じテレフォニー ダイヤル プランを使用している別のユーザーに電話をかけるときに 4 桁の内線番号をダイヤルしている場合は、内線番号の桁数として 4 を選択します。
        
        このフィールドは、1 ～ 20 の値を設定できる必須のボックスです。一般的な内線番号の桁数は 3 ～ 7 です。既存のテレフォニー環境で内線番号が使用されている場合は、それらの内線番号と同じ桁数を指定する必要があります。
        
        セッション開始プロトコル (SIP) または E.164 ダイヤル プランを作成して、UM が有効なユーザーにダイヤル プランを関連付けた場合でも、ユーザーが使用する内線番号を入力する必要があります。この番号は、Outlook Voice Access ユーザーがメールボックスにアクセスするときに使用します。
    
      - <strong>ダイヤル プランの種類</strong> URI (Uniform Resource Identifier) は、リソースを識別または指定する文字列です。この識別子の主な目的は、VoIP デバイスが特定のプロトコルを使用して他のデバイスとネットワークを介して通信できるようにすることです。URI はスキームで定義されており、スキームは特定の構文と形式および呼び出しのプロトコルを定義しています。単純に言うと、この形式は IP PBX または PBX から渡されます。UM ダイヤル プランを作成した後は、ダイヤル プランを削除して、正しい種類のダイヤル プランを作り直さなければ、ダイヤル プランの種類を変更できません。次のいずれかの種類のダイヤル プランを選択できます。
        
          - <strong>内線電話番号</strong>   これは、最も一般的な URI の種類です。VoIP ゲートウェイまたは IP 構内交換機 (PBX) からの発信元と発信先の情報は、次のいずれかの形式で一覧表示されます。Tel:512345 または 512345@\<*IP address*\>。これは、ダイヤル プランの既定の URI の種類です。
        
          - <strong>SIP URI</strong> セッション開始プロトコル (SIP) ルーティングをサポートする IP PBX などの SIP URI ダイヤル プランが必要な場合、または Microsoft Office Communications Server 2007 R2 または Microsoft Lync Server とユニファイド メッセージングを統合する場合は、この種類の URI を使用します。VoIP ゲートウェイ、IP PBX、Communications Server 2007 R2、または Lync Server からの呼び出し元および呼び出し先情報は、次の形式で SIP アドレスとして一覧表示されます。SIP:\<*username*\>@\<*domain* または *IP address*\>:ポート。
        
          - <strong>E.164</strong>   E.164 は公衆電話システム用の国際番号付けプランであり、割り当てられる各番号には、国コード、国内宛先コード、および加入者番号が含まれます。VoIP ゲートウェイまたは IP PBX から送信される発信元情報および発信先情報は、次の形式で一覧表示されます。Tel:+14255550123。
        

        > [!WARNING]
        > ダイヤル プランを作成した後で URI タイプを変更するには、ダイヤル プランを削除してから再作成して、正しい URI タイプを含める必要があります。

    
      - <strong>VoIP セキュリティ モード</strong>   このドロップダウン リストで、UM ダイヤル プランの VoIP セキュリティ設定を選択します。ダイヤル プランに対して次のいずれかのセキュリティ設定を選択できます。
        
          - <strong>セキュリティ保護なし</strong>   既定では、UM ダイヤル プランを作成した時点で SIP 信号または RTP トラフィックの暗号化がなしに設定されます。セキュリティで保護されないモードの場合、UM ダイヤル プランに関連付けられたクライアント アクセス サーバーおよびメールボックス サーバーは、暗号化を使用せずに、VoIP ゲートウェイ、IP PBX、SBC、およびその他のクライアント アクセス サーバーおよびメールボックス サーバーとデータを送受信します。セキュリティで保護されないモードでは、リアルタイム転送プロトコル (RTP) メディア チャネルばかりでなく SIP 信号情報も暗号化されません。
        
          - <strong>セキュリティで保護された SIP</strong>   <strong>セキュリティで保護された SIP</strong> を選択すると、SIP 信号トラフィックのみが暗号化され、RTP メディア チャネルは依然として TCP を使用し、暗号化されません。SIP がセキュリティで保護されている場合、SIP 信号トラフィックおよび VoIP データの暗号化には、相互トランスポート層セキュリティ (TLS) が使用されます。
        
          - <strong>セキュリティで保護</strong>   <strong>セキュリティで保護</strong> を選択すると、SIP 信号トラフィックと RTP メディア チャネルの両方が暗号化されます。SRTP (Secure Realtime Transport Protocol) を使用する、セキュリティで保護された信号メディア チャネルと SIP 信号トラフィックの両方で、相互 TLS を使用して VoIP データが暗号化されます。
    
      - <strong>音声の言語</strong>   この一覧を使用して Outlook Voice Access ユーザーが使用する既定の言語を指定します。この設定は、UM 自動応答の言語設定には適用されません。Outlook Voice Access の言語は、UM 自動応答に使われる言語と同じ言語にも違う言語にも設定できます。ダイヤル プランに関連付けられたユーザーに電話をかける場合、音声言語は、音声録音されたオペレーターが使用する既定の言語になります。発信者が聞くシステム プロンプトも同じ言語で再生されます。UM ダイヤル プランで選択した言語は、電子メール、ボイス メール、予定表アイテムを読んだり、個人用の案内応答が録音されていない場合にユーザー名を通知したり、ボイス メール プレビュー機能を使用して音声メッセージをトランスクリプト化したり、自動音声認識 (ASR) が正しく動作するようにしたりするのに使用されます。
    
      - <strong>国/地域コード</strong>   発信呼び出しに使用される国/地域コードを入力するには、このボックスを使用します。この番号は、ダイヤルされた電話番号の前に付加されます。このボックスには、1 ～ 4 桁の数値を入力できます。たとえば、米国内の国/地域コードは 1、英国内の国/地域コードは 44 です。

3.  <strong>保存</strong> をクリックします。

## シェルを使用して UM ダイヤル プランを作成する

この例では、4 桁の内線番号を使用する、`MyUMDialPlan` という名前の UM ダイヤル プランを新しく作成します。

    New-UMDialplan -Name MyUMDialPlan -NumberofDigits 4

この例では、5 桁の内線番号を使用して SIP URI をサポートする、`MyUMDialPlan` という名前の UM ダイヤル プランを新しく作成します。

    New-UMDialplan -Name MyUMDialPlan -UriType SIPName -NumberofDigits 5

