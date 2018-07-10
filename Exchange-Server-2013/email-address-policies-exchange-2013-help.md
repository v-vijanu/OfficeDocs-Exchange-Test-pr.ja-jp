﻿---
title: '電子メール アドレス ポリシー: Exchange 2013 Help'
TOCTitle: 電子メール アドレス ポリシー
ms:assetid: b63b63bb-6faf-4337-8441-50bc64b49bb8
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Bb232171(v=EXCHG.150)
ms:contentKeyID: 49896430
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 電子メール アドレス ポリシー

 

_**適用先:**Exchange Server 2013_

_**トピックの最終更新日:**2016-07-21_

受信者 (ユーザー、リソース、連絡先、およびグループを含む) とは、Microsoft Exchange がメッセージを配信またはルーティングできる Active Directory のメールが有効な任意のオブジェクトのことです。受信者が電子メール メッセージを送受信するには、電子メール アドレスが必要です。電子メール アドレス ポリシーによって、受信者のプライマリ電子メール アドレスとセカンダリ電子メール アドレスが生成され、電子メールを送受信できるようになります。

既定では、Exchange にはメールが有効な各ユーザー向けの電子メール アドレス ポリシーが含まれています。この既定のポリシーでは、電子メール アドレスのローカル部分として受信者のエイリアスを指定し、既定の承認済みドメインを使用します。電子メール アドレスのローカル部分は、アット マーク (@) の前に表示される名前です。ただし、受信者の電子メール アドレスの表示方法を変更できます。たとえば、電子メール アドレスを *firstname*.*lastname*@contoso.com のように表示することを指定できます。

また、すべての受信者または一部の受信者にのみ追加の電子メール アドレスを指定する場合は、既定のポリシーを変更することも、追加のポリシーを作成することもできます。たとえば、David Hamilton のユーザー メールボックスは、hdavid@mail.contoso.com に宛てた電子メール メッセージと hamilton.david@mail.contoso.com に宛てた電子メール メッセージを受信できます。

電子メール アドレス ポリシーに関連する管理タスクについては、「[電子メール アドレス ポリシーの手順](email-address-policy-procedures-exchange-2013-help.md)」を参照してください。

## 受信者ポリシーの動作

Exchange では、受信者フィルター条件に一致するすべての受信者にポリシーが適用されます。

  - 複数の受信者ポリシーは、最高の優先度のものから最低の優先度のものへの順で適用されます。複数のポリシー間で競合が発生した場合は、最高の優先度を持つポリシーが適用されます。既定の受信者ポリシーは、常に最低の優先度を持ち、その他に一致するポリシーがない場合に適用されます。
    
    受信者ポリシーの作成時に、明示的に優先度を指定していないと、そのポリシーは最高の優先度として追加されます。既存のポリシーに関連付けられている優先度を指定すると、既存のポリシーと、それ以下の優先度を持つすべてのポリシーは優先度が 1 つずつ下げられます。新しいポリシーは、指定した優先度に挿入されます。
    
    受信者ポリシー機能は、電子メール アドレス ポリシーと承認済みドメインの 2 つの機能に分割されています。承認済みドメインの詳細については、「[承認済みドメイン](accepted-domains-exchange-2013-help.md)」を参照してください。

  - Exchange 管理シェルで **Update-EmailAddressPolicy** コマンドレットを実行すると、電子メール アドレス ポリシーを使用して受信者オブジェクトが更新されます。

  - 受信者オブジェクトを変更して保存するたびに、Exchange によって電子メール アドレスの条件および設定が適切に適用されます。電子メール アドレス ポリシーを変更して保存すると、関連付けられたすべての受信者に変更が反映されます。また、受信者オブジェクトが変更されると、その受信者の電子メール アドレス ポリシーのメンバーシップが再評価され、適用されます。

## 電子メール アドレス ポリシーの作成

電子メール アドレス ポリシーの作成では、次の電子メール アドレスの種類を使用できます。

  - **既定の SMTP 電子メール アドレス**。*既定*の SMTP 電子メール アドレスは、既に用意されている一般的に使用される電子メール アドレスの種類です。

  - **カスタム SMTP 電子メール アドレス**。既定の SMTP 電子メール アドレスを使用しない場合、カスタム SMTP 電子メール アドレスを指定できます。
    
    カスタム SMTP 電子メール アドレスを作成する場合、次の表の変数を使用して電子メール アドレスのローカル部分に代替値を指定できます。
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>変数</th>
    <th>値</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>%g</p></td>
    <td><p>名 (姓名の名)</p></td>
    </tr>
    <tr class="even">
    <td><p>%i</p></td>
    <td><p>ミドル ネームのイニシャル</p></td>
    </tr>
    <tr class="odd">
    <td><p>%s</p></td>
    <td><p>姓 (名字)</p></td>
    </tr>
    <tr class="even">
    <td><p>%d</p></td>
    <td><p>表示名</p></td>
    </tr>
    <tr class="odd">
    <td><p>%m</p></td>
    <td><p>Exchange エイリアス</p></td>
    </tr>
    <tr class="even">
    <td><p>%<em>x</em>s</p></td>
    <td><p>姓から最初の <em>x</em> 文字を使用します。たとえば、<em>x</em> が 2 の場合、姓の最初の 2 文字が使用されます。</p></td>
    </tr>
    <tr class="odd">
    <td><p>%<em>x</em>g</p></td>
    <td><p>名から最初の <em>x</em> 文字を使用します。たとえば、<em>x</em> が 2 の場合、名の最初の 2 文字が使用されます。</p></td>
    </tr>
    </tbody>
    </table>


  - **SMTP 以外の電子メール アドレス**。SMTP 以外の電子メール アドレスでは、次の種類がサポートされます。
    
      - EX (従来の DN プロキシ アドレス プレフィックス DisplayName)
    
      - X.500
    
      - X.400
    
      - MSMail
    
      - CcMail
    
      - ロータス ノーツ
    
      - Novell GroupWise
    
      - Exchange ユニファイド メッセージング プロキシ アドレス (EUM プロキシ アドレス)
    

    > [!IMPORTANT]
    > Exchange では、SMTP 以外の電子メール アドレスはすべてカスタム アドレスと見なされます。X.400、GroupWise、ロータス ノーツなどの電子メール アドレスの種類に固有のダイアログ ボックスやプロパティ ページは、Exchange には用意されていません。SMTP 以外のカスタム電子メール アドレスを追加する場合は、適切な DLL (ダイナミック リンク ライブラリ) ファイルが必要になります。適切な DLL ファイルがないと、カスタマイズされた電子メール アドレス ポリシーを作成することはできません。以下のエラーがイベント ビューアーのログに記録されます。"コンピューター 'i386' 上のアドレスの種類 'SADF' に対する、Microsoft Exchange ディレクトリ内の電子メール アドレス記述オブジェクトが見つかりません。"



電子メール アドレス ポリシーを作成する詳細な手順については、以下のトピックを参照してください。

[電子メール アドレス ポリシーの作成](create-an-email-address-policy-exchange-2013-help.md)

[受信者フィルターを使用した電子メール アドレス ポリシーの作成](create-an-email-address-policy-by-using-recipient-filters-exchange-2013-help.md)
