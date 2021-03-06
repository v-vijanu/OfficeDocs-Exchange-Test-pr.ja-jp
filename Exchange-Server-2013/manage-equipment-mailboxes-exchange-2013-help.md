﻿---
title: '備品用メールボックスの管理: Exchange Online Help'
TOCTitle: 備品用メールボックスの管理
ms:assetid: e5f58b3a-83e1-4742-8846-85103a44ee18
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ215770(v=EXCHG.150)
ms:contentKeyID: 48270180
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 備品用メールボックスの管理

 

_**適用先:** Exchange Online, Exchange Server 2013_

*備品用メールボックス*は、ポータブル コンピューター、プロジェクター、マイク、社用車などの特定の場所にないリソースに割り当てられるリソース メールボックスです。管理者が備品用メールボックスを作成した後には、ユーザーは該当する備品用メールボックスを会議出席依頼に含めることによって、備品を簡単に予約できます。EAC およびシェルを使用して、備品用メールボックスの作成または備品用メールボックスのプロパティの変更を行えます。詳細については、「[受信者](recipients-exchange-2013-help.md)」を参照してください。

別の種類のリソース メールボックス、会議室メールボックスについては、「[会議室メールボックスの作成と管理](create-and-manage-room-mailboxes-exchange-2013-help.md)」を参照してください。

## 始める前に把握しておくべき情報

  - 予想所要時間 : 2 ～ 5 分。

  - この手順を実行する際には、あらかじめアクセス許可を割り当てる必要があります。必要なアクセス許可の一覧については、以下を参照してください。「[受信者のアクセス許可](recipients-permissions-exchange-2013-help.md)」の「受信者プロビジョニングのアクセス許可」。

  - このトピックの手順で使用可能なキーボード ショートカットについては、「[Exchange 管理センターのキーボード ショートカット](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)」を参照してください。


> [!TIP]
> 問題がある場合は、Exchange のフォーラムで質問してください。 次のフォーラムにアクセスしてください。<A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>、 <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>、 または <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>。.



## 必要な作業

## 備品用メールボックスを作成する

## EAC を使用して備品用メールボックスを作成する

1.  EAC で、<strong>受信者</strong> \> <strong>リソース</strong> に移動します。

2.  備品用メールボックスを作成するには、\[**新規**\] \> \[**備品用メールボックス**\] をクリックしてください。会議室メールボックスを作成するには、\[**新規**\] \> \[**会議室メールボックス**\] をクリックしてください。

3.  新しいリソース メールボックスの設定を指定するには、ページのオプションを使用します。
    
      - **\* \[備品名</strong>   このボックスを使用して、備品用メールボックスの名前を入力します。これは、EAC のリソース メールボックス リストおよび組織のアドレス帳にリストされる名前です。この名前は必須であり、64 文字以下にする必要があります。
        

        > [!TIP]
        > 会議室の詳細を示す [定員] などの他のフィールドもありますが、一貫性のある名前付け規則を使用して、最も重要な詳細を備品名に集約するようにしてください。理由は、ユーザーが会議出席依頼のアドレス帳から備品を選択するときに詳細を簡単に確認できるようにするためです。

    
      - **\* \[電子メール アドレス</strong>   備品用メールボックスには、予約の依頼を受信するための電子メール アドレスがあります。電子メール アドレスは、@ 記号の左側のエイリアス (フォレスト内で一意にする必要がある) および右側のドメイン名から構成されます。電子メール アドレスは必須です。

4.  完了したら、<strong>保存</strong> をクリックして備品用メールボックスを作成します。

備品用メールボックスを作成したら、備品用メールボックスを編集して、予約オプション、メール ヒント、および委任に関する情報を更新することができます。会議室メールボックス プロパティを変更するには、以下にある「備品用メールボックスのプロパティを変更する」セクションを参照してください。

## シェルを使用して備品用メールボックスを作成する

この例では、次の構成を持つ備品用メールボックスが作成されます。

  - 備品用メールボックスが Mailbox Database 1 にある。

  - 備品名は MotorVehicle2 であり、GAL では 名前が Motor Vehicle 2 として表示される。

  - 電子メール アドレスは MotorVehicle2@contoso.com である。

  - メールボックスが Equipment という組織単位にある。

  - *Equipment* パラメーターによって、このメールボックスが備品用メールボックスとして作成されることが指定される。

<!-- end list -->

    New-Mailbox -Database "Mailbox Database 1" -Name MotorVehicle2 -OrganizationalUnit Equipment -DisplayName "Motor Vehicle 2" -Equipment

構文およびパラメーターの詳細については、「[New-Mailbox](https://technet.microsoft.com/ja-jp/library/aa997663\(v=exchg.150\))」を参照してください。

## 正常な動作を確認する方法

ユーザーのメールボックスが正常に作成されたことを確認するには、次のいずれかを実行します。

  - EAC で、<strong>受信者</strong> \> <strong>リソース</strong> に移動します。新しいユーザーのメールボックスは、メールボックスの一覧で表示されます。<strong>メールボックスの種類</strong> の種類は、<strong>備品用</strong> と表示されます。

  - シェルで次のコマンドを実行して、新しい備品用メールボックスに関する情報を表示します。
    
        Get-Mailbox <Name> | FL Name,RecipientTypeDetails,PrimarySmtpAddress

## 備品用メールボックスのプロパティを変更する

備品用メールボックスを作成した後、EAC またはシェルを使用して変更したり、追加のプロパティを設定したりすることができます。

## EAC を使用して備品用メールボックスのプロパティを変更する

1.  EAC で、<strong>受信者</strong> \> <strong>リソース</strong> に移動します。

2.  リソース メールボックス の一覧で、プロパティを変更する備品用メールボックスをクリックし、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。

3.  備品用メールボックスのプロパティ ページで、次のセクションのいずれかをクリックして、プロパティを表示または変更します。
    
      - 全般
    
      - デリゲート
    
      - 予約オプション
    
      - 連絡先の情報
    
      - 電子メール アドレス
    
      - メール ヒント

## 全般

<strong>全般</strong> セクションを使用し、リソースに関する基本情報を表示または変更します。

  - **\* \[備品名</strong>   この名前は、EAC のリソース メールボックス リストおよび組織のアドレス帳に表示されます。変更する場合、64 文字を超えることはできません。

  - **\* \[電子メール アドレス</strong>   この読み取り専用ボックスには、備品用メールボックスの電子メール アドレスが表示されます。「電子メール アドレス」セクションで変更できます。

  - <strong>定員</strong>   このボックスを使用して、このリソースを使用できる最大人数を必要に応じて入力します。たとえば、備品用メールボックスがコンパクト カーに対応する場合は、**4** を入力できます。

<strong>その他のオプション</strong> をクリックして、これらの追加プロパティを表示または変更します。

  - <strong>組織単位</strong>   この読み取り専用ボックスには、備品用メールボックスのアカウントを含む組織単位 (OU) が表示されます。Active Directory のユーザーとコンピューターを使用し、別の OU にアカウントを移動する必要があります。

  - <strong>メールボックス データベース</strong>   この読み取り専用ボックスには、備品用メールボックスをホストするメールボックス データベースの名前が表示されます。EAC の <strong>移行</strong> ページを使用し、別のデータベースにメールボックスを移動します。

  - **\* \[エイリアス</strong>   このボックスを使用して、備品用メールボックスのエイリアスを変更します。

  - <strong>アドレス一覧に表示しない</strong>   アドレス一覧や、Exchange 組織で定義されているその他のアドレス一覧に備品用メールボックスが表示されないようにするには、このチェック ボックスをオンにします。このチェック ボックスをオンにした後も、ユーザーは電子メール アドレスを使用して、この備品用メールボックスに予約メッセージを送信できます。

  - <strong>部署</strong>   このボックスを使用して、リソースを関連付ける部署名を指定します。このプロパティを使用すると、動的配布グループおよびアドレス一覧に関する受信者の条件を作成できます。

  - <strong>会社</strong>   このボックスを使用して、リソースを関連付ける会社を指定します。Department プロパティと同じように、このプロパティを使用すると、動的配布グループおよびアドレス一覧に関する受信者の条件を作成できます。

  - <strong>アドレス帳ポリシー</strong>   リソースのアドレス帳ポリシー (ABP) を指定するには、このオプションを使用します。ABP には、グローバル アドレス一覧 (GAL)、オフライン アドレス帳 (OAB)、会議室一覧、およびアドレス一覧のセットが含まれます。詳細については、「[アドレス帳ポリシー](address-book-policies-exchange-2013-help.md)」を参照してください。
    
    ドロップダウン リストから、このメールボックスに関連付けるポリシーを選択します。

  - <strong>カスタム属性</strong>   このセクションには、備品用メールボックスに対して定義されたカスタム属性が表示されます。カスタム属性の値を指定するには、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックします。受信者に対して最大 15 のカスタム属性を指定できます。

## デリゲート

このセクションを使用して、備品用メールボックスで予約の依頼を処理する方法、および予約の依頼を承諾または拒否できるユーザー (承諾/拒否が自動的に行われない場合) を定義する方法を表示または変更します。

  - <strong>予約の依頼</strong>   次のいずれかのオプションを選択し、予約の依頼を処理します。
    
      - <strong>Accept or decline booking requests automatically (予約の依頼を自動的に承諾または辞退する)</strong>   有効な会議出席依頼の場合は、リソースが自動的に予約されます。既存の予約とスケジュールが重複する場合、または予約の依頼がリソースのスケジュール制限に違反する場合 (予約期間が長すぎる場合など) は、会議出席依頼が自動的に拒否されます。
    
      - <strong>予約の依頼を承諾または拒否できる代理人を選択する</strong>   リソースの代理人は、備品用メールボックスに送信される会議出席依頼を承諾または拒否します。複数のリソースの代理人を割り当てる場合、1 つの会議出席依頼を複数のリソースの代理人が操作することはできません。

  - <strong>代理人</strong>   予約の依頼を代理人に送信することを要求するオプションを選択した場合は、指定された代理人が表示されます。<strong>追加</strong>![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") または <strong>削除</strong>![\[削除\] アイコン](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "[削除] アイコン") をクリックし、このリストで代理人を追加したり削除したりします。

## 予約オプション

<strong>予約オプション</strong> の選択肢を使用して、リソースをスケジュールできる時間帯、リソースを予約できる時間の長さ、およびリソースをいつから事前に予約できるかを定義する予約ポリシーの設定を、表示または変更します。

  - <strong>定期的な会議を許可する</strong>   この設定により、リソースにおける定期的な会議を許可または禁止します。既定では、この設定は有効になっているので、定期的な会議は許可されます。

  - <strong>稼働時間内にのみスケジュールの設定を許可する</strong>   この設定により、リソースに対して定義された稼働時間内ではない会議出席依頼を許可または禁止します。既定では、この設定は無効であり、勤務時間外の会議出席依頼が許可されます。既定の勤務時間は、月曜日から金曜日の午前 8 時から午後 5 時です。備品用メールボックスの稼働時間は、\[予定表\] ページの \[デザイン\] セクションで構成できます。

  - <strong>終了日がこの制限を超える場合は常に辞退する</strong>   この設定では、予約の最大リード タイム設定によって指定される日付を超える定期的な会議の動作を制御します。
    
      - この設定を有効にすると、<strong>Maximum booking lead time (予約の最大リード タイム)</strong> ボックスの値によって指定される日付以前に予約が始まって、予約が指定日を超える場合、定期的な予約の依頼は自動的に辞退されます。これは既定の設定です。
    
      - この設定を無効にすると、**最長予約リード タイム</strong> ボックスの値によって指定される日付以前に予約の依頼が始まって、予約が指定日を超える場合、定期的な予約の依頼は自動的に許可されます。ただし、予約の数は、指定された日付の後に予約が行われないように削減されます。

  - <strong>最長予約リード タイム (日)</strong>   この設定では、リソースを事前に予約できる最大日数を指定します。有効な入力値は 0 ～ 1080 の整数です。既定値は 180 日です。

  - <strong>最大期間 (時間)</strong>   この設定では、予約の依頼においてリソースを予約できる最大期間を指定します。既定値は 24 時間です。
    
    定期的な予約の依頼の場合、予約の最大時間は、定期的な予約の依頼の各回の長さに適用されます。

このページには、会議出席依頼を送信してリソースを予約するユーザーに送信されるメッセージを入力できるボックスもあります。

## 連絡先の情報

<strong>連絡先の情報</strong> セクションを使用して、リソースの連絡先情報を表示または変更します。このページの情報がアドレス帳に表示されます。


> [!TIP]
> <STRONG>[都道府県]</STRONG> ボックスを使用すると、動的配布グループ、電子メール アドレス ポリシー、またはアドレス一覧に関する受信者の条件を作成できます。



## 電子メール アドレス

<strong>電子メール アドレス</strong> セクションを使用して、備品用メールボックスに関連付けられた電子メール アドレスを表示または変更します。これには、メールボックスのプライマリ SMTP アドレスおよび関連するすべてのプロキシ アドレスが含まれます。プライマリ SMTP アドレス (*返信アドレス*とも呼ばれます) は、アドレス一覧に太字で表示され、<strong>種類</strong> 列に大文字の **SMTP** 値が表示されます。

  - <strong>追加</strong> <strong>追加</strong> ![\[追加\] アイコン](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "[追加] アイコン") をクリックして、このメールボックスの新しい電子メール アドレスを追加します。次のいずれかのアドレスの種類を選択します。
    
      - <strong>SMTP</strong>   これは既定のアドレスの種類です。このボタンをクリックし、**\* \[電子メール アドレス</strong> ボックスに SMTP アドレスを入力します。
    
      - <strong>EUM</strong>   EUM (Exchange ユニファイド メッセージング) アドレスは、Exchange 組織内の UM が有効な受信者を検索するために、Microsoft Exchange ユニファイド メッセージング サービスによって使用されます。EUM アドレスには、UM が有効なユーザーの内線番号と UM ダイヤル プランが含まれています。このボタンをクリックして、<strong>アドレス/内線番号</strong> ボックスに内線番号を入力します。<strong>参照</strong> をクリックし、メールボックスのダイヤル プランを選択します。
    
      - <strong>カスタム アドレス</strong>   このボタンをクリックし、サポートされる SMTP 以外の電子メール アドレスのいずれかを **\* \[電子メール アドレス</strong> ボックスに入力します。
        

        > [!NOTE]
        > X.400 アドレスを除き、Exchange は、カスタム アドレスが適切な形式かどうかを検証しません。指定するカスタム アドレスが、そのアドレスの種類の書式要件に従っていることを確認する必要があります。

    

    > [!NOTE]
    > 新しい電子メール アドレスを追加するときは、それをプライマリ SMTP アドレスにすることを選択できます。



  - <strong>この受信者に適用されるメール アドレス ポリシーに基づいてメール アドレスを自動更新する</strong>   組織の電子メール アドレス ポリシーに加えられた変更に基づいて受信者の電子メール アドレスを自動的に更新するには、このチェック ボックスをオンにします。

## メール ヒント

<strong>メール ヒント</strong> セクションを使用して、備品用メールボックスに予約の依頼を送信する前に、問題が発生する可能性があるユーザーに警告するためのメール ヒントを追加します。メール ヒントは、この受信者が新しい電子メール メッセージの \[宛先\]、\[CC\]、または \[BCC\] 行に追加されたときに情報バーに表示されるテキストです。


> [!NOTE]
> メール ヒントに HTML タグを入れることはできますが、スクリプトは許可されません。カスタム メール ヒントの長さは 175 文字 を超えることはできません。これは表示文字数で、HTML タグは含まれません。



## シェルを使用して備品用メールボックスのプロパティを変更する

備品用メールボックスのプロパティを表示および変更するには、次の組み合わせのコマンドレットを使用します。**Get-Mailbox** コマンドレットおよび **Set-Mailbox** コマンドレットを使用し、備品用メールボックスの一般的なプロパティおよび電子メールを表示、変更します。**Get-CalendarProcessing** コマンドレットおよび **Set-CalendarProcessing** コマンドレットを使用し、代理人および予約オプションを表示、変更します。

  - **Get-User** および **Set-User**   これらのコマンドレットを使用し、部署や会社名などの一般的なプロパティを表示、設定します。

  - **Get-Mailbox** および **Set-Mailbox**   このコマンドレットを使用し、電子メール アドレスやメールボックス データベースなどのメールボックス プロパティを表示、設定します。

  - **Get-CalendarProcessing** および **Set-CalendarProcessing**   このコマンドレットを使用し、予約オプションおよび代理人を表示、設定します。

このコマンドレットの詳細については、以下のトピックを参照してください。

  - [Get-User](https://technet.microsoft.com/ja-jp/library/aa996896\(v=exchg.150\))

  - [Set-User](https://technet.microsoft.com/ja-jp/library/aa998221\(v=exchg.150\))

  - [Get-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123685\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/ja-jp/library/bb123981\(v=exchg.150\))

  - [Get-CalendarProcessing](https://technet.microsoft.com/ja-jp/library/dd298137\(v=exchg.150\))

  - [Set-CalendarProcessing](https://technet.microsoft.com/ja-jp/library/dd335046\(v=exchg.150\))

次に、シェルを使用して備品用メールボックスのプロパティを変更する場合の、いくつかの例を示します。

この例では、MotorPool 1 という備品用メールボックスの表示名および プライマリ SMTP アドレス (既定の返信アドレスとも呼ばれる) を変更します。以前の返信アドレスはプロキシ アドレスとして保持されます。

    Set-Mailbox "MotorPool 1" -DisplayName "Motor Pool 1 - Compact" -EmailAddresses SMTP:MP1.compact@contoso.com,smtp:MP.1@contoso.com

この例では、稼働時間内にのみスケジュールすることを予約の依頼に対して許可するように、備品用メールボックスを構成します。

    Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'EquipmentMailbox')} | Set-CalendarProcessing -ScheduleOnlyDuringWorkHours $true

この例では、**Get-User** コマンドレットを使用して Audio Visual 部署のすべてのすべての備品用メールボックスを検索した後、**Set-CalendarProcessing** コマンドレットを使用して、承諾または拒否を行う Ann Beebe という名前の代理人に予約の依頼を送信します。

    Get-User -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'EquipmentMailbox') -and (Department -eq 'Audio Visual')} | Set-CalendarProcessing -AllBookInPolicy $false -AllRequestInPolicy $true -ResourceDelegates "Ann Beebe"

## 正常な動作を確認する方法

備品用メールボックスのプロパティが正常に構成されたことを確認するには、次の手順を実行します。

  - EAC でメールボックスを選択し、<strong>編集</strong>![編集アイコン](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "編集アイコン") をクリックすると、変更したプロパティまたは機能を表示できます。変更したプロパティによっては、選択したメールボックスの \[詳細\] ウィンドウに表示される場合があります。

  - シェルで **Get-Mailbox** コマンドレットを使用して、変更を確認します。シェルを使用する場合の利点の 1 つは、複数のメールボックスの複数のプロパティを参照できるというものです。予約の依頼を稼働時間内にのみスケジュールできる上記の例では、次のコマンドの実行により新しい値が確認されます。
    
        Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'EquipmentMailbox')} | Get-CalendarProcessing | fl Identity,ScheduleOnlyDuringWorkHours

