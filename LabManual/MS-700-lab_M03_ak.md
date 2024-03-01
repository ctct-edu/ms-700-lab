

# **ラボ 03: Teams のチーム、コラボレーション、アプリ設定を管理する**

# **学生ラボの解答集**

## **ラボのシナリオ**

このコースのラボでは、Contoso Ltd のチーム管理者である Joni Sherman の役割を引き受けます。このラボでは、チームの作成と変更、メンバーシップの管理、削除されたチームの回復など、Teams 管理者として運用タスクを実行します。

Microsoft Teams でのコラボレーションの管理では、チーム設定やプライベート チャネル作成ポリシーなどのチャットとコラボレーション エクスペリエンスを管理します。最後に、アプリのアクセス許可やアプリのセットアップ ポリシー、アプリ、ボット、コネクタなどの Teams アプリの設定を Microsoft Teams で管理したり、Microsoft Teams でカスタム アプリを公開したりします。

## **目標**

このラボを完了すると、次のことができるようになります。

- Microsoft 365 グループからチームを作成する
- PowerShell を使用してチームを作成する
- Microsoft Graph API を使用してチームを作成する
- 動的メンバーシップを持つチームを作成する
- Teams のアーカイブとアーカイブ解除
- チームの削除と復元
- メッセージング・ポリシーの作成
- プライベート チャネルを管理する
- サードパーティのストレージプロバイダーを無効にする
- ポリシーパッケージの管理
- 既定の組織全体のアプリ ポリシーを編集してテストする
- 既定のアプリのアクセス許可ポリシーを編集してテストする
- カスタム アプリのセットアップ ポリシーを作成して管理する

## **ラボのセットアップ**

- **所要時間:** 110 分

## **指示**

### **演習 1: チームのリソースを管理する**

#### タスク 1 - 既存の Microsoft 365 グループからチームを作成する

Contoso のパイロット プロジェクトの一環として、以前のラボで作成した **IT 部門の** Microsoft 365 グループを変更し、Teams 機能を追加する必要があります。

1. 提供された資格情報を使用して**クライアント 1 VM** に接続します。
2. タスク バーの Teams アイコンを選択して **Teams** デスクトップ クライアントを起動し、**Joni Sherman** (JoniS@YourTenant.OnMicrosoft.com)でサインインします。「Stay signed in to all your apps」のウィンドウでは **「No,sign in to this app only」** をクリックします。
3. 左側のナビゲーション ウィンドウで、[**Teams**] を選択し、画面上の方に表示される **[+]** を選択し、ウィンドウの中央から [**Create Team**] を選択します。
4. [Create Team] 画面の左側にあるで、 **[From group]** を選択します。
5.  **[Which Microsoft 365 group do you want to use?]** ダイアログで、グループ "**IT-Department"** を選択し、**[Add team]** を選択します。**「Creating the team...」** プロセスが完了するまで待ちます。
6. 左側のウィンドウで新しい"**IT-Department"**チーム名の右に表示されるから 3 つのドット (**...**) を選択し、[**Manage team**] を選択します。
7. チームの所有者とメンバーを確認します。
   - オーナー: **Joni Sherman**
   - メンバーとゲスト:　**Allan Deyoung** , **MOD Administrator** and **Patti Fernandezr**
8. Teams デスクトップ クライアントを開いたままにして、次のタスクに進みます。

既存の Microsoft 365 グループを使用して、Teams デスクトップ クライアントで新しいチームを正常に作成しました。Teams クライアントを開いたままにして、次のタスクに進みます。

#### タスク 2 - PowerShell を使用してチームを作成する

このタスクでは、Teams PowerShell を使用して新しいチーム "**CA-Office"** を作成します。パブリックチャンネル **「Support」** と **「Recruiting」** を作成します。さらに、Teams PowerShell を使用してプライベート チャネル **「Administration」** を作成します。

1. 提供された資格情報を使用して**クライアント 1 VM** に接続します。

2. ページ下部のタスク バーで、[スタート] ボタンを右クリックし、**[Windows PowerShell]** を選択します。

3. 次のコマンドレットを実行して、テナント内の Microsoft Teams に接続します。

   ```
   Connect-MicrosoftTeams
   ```

4. **[サインイン**] ダイアログ ボックスが開きます。提供された **Joni Sherman** の資格情報の **UPN** (例: JoniS@YourTenant.onmicrosoft.com) を入力し、[**次へ**] を選択します。

5. [**パスワードの入力**] ダイアログ ボックスで、提供された **Joni Sherman** の資格情報の**パスワード**を入力し、[**サインイン**] を選択します。

6. PowerShell ウィンドウに次のコマンドレットを入力して、新しいチーム **CA-Office** を作成します。

   ```
   New-Team -Displayname "CA-Office" -MailNickName "CA-Office" -Visibility Public
   ```

   

7. ユーザー **Alex Wilber** をチームに追加するには、次のコマンドレットを入力します (「YourTenant」は提供された Microsoft 365 テナントの名前に置き換えます)。

   ```
   Get-Team -Displayname "CA-Office" | Add-TeamUser -User AlexW@YourTenant.OnMicrosoft.com
   ```

   

8. ユーザー **Allan Deyoung** をチームに追加するには、次のコマンドレットを入力します  (「YourTenant」は提供された Microsoft 365 テナントの名前に置き換えます)。

   ```
   Get-Team -Displayname "CA-Office" | Add-TeamUser -User AllanD@YourTenant.onmicrosoft.com
   ```

   

9. 次のコマンドレットを使用して、**CA-Office** チームで**チャネル Support** を作成します。

   ```
   Get-Team -Displayname "CA-Office" | New-TeamChannel -DisplayName "Support"
   ```

   

10. 次のコマンドレットを使用して、**CA-Office** チームで別のチャネル **Recruiting** を作成します。

    ```
    Get-Team -Displayname "CA-Office" | New-TeamChannel -DisplayName "Recruiting"
    ```

    

11. 次のコマンドレットを使用して、**CA-Office** チームでプライベート チャネル**管理**を作成します。

    ```
    Get-Team -Displayname "CA-Office" | New-TeamChannel -DisplayName "Administration" -MembershipType Private
    ```

    

12. Microsoft Teams 環境から切断します。

    ```
    Disconnect-MicrosoftTeams
    ```

    

13. PowerShell ウィンドウを閉じます。

14. タスク バーから Teams デスクトップ クライアントを開きます。すべてのチームの左側のペインで、Joni は新しい **CA-Office** チームのメンバーであり、その下に "Administration" という名前のプライベート チャネルが表示されます。

15. すべてのブラウザー ウィンドウと Teams デスクトップ クライアントを閉じます。

これで、Alex Wilber と Allan Deyoung というメンバーからなる **CA-Office** という名前のチームが作成されました。ジョニ・シャーマンは唯一のチームオーナーです。PowerShell コマンドレットで所有者を指定しておらず、Joni のコンテキストで実行されたため、Joni が自動的に所有者として追加されたことに注意してください。さらに、**「Support」** と **「Recruiting」** という名前のパブリックチャンネルと、 **「Administration」** という名前のプライベートチャンネルを作成しました。

#### タスク 3 - Graph API を使用してチームを作成する

このタスクでは、Teams を使用して組織の特定の自動化プランの Graph API 機能をテストします。このタスクでは、パブリック参加オプションなどの最小限の設定を持つ **Early Adopters** という新しいチームと、**Tech Meetings** と呼ばれる複数の既存のチャネルを持つ別のチームを作成します。

1. 提供された資格情報を使用して**クライアント 1 VM** に接続します。

2. Microsoft Edge を開き、ブラウザーを最大化して、次の **Graph エクスプローラー**に移動します https://developer.microsoft.com/graph/graph-explorer

3. ページの右上にある人の形のアイコンをを選択し、**Joni Sherman** (JoniS@YourTenant.onmicrosoft.com) としてサインインします。

4. Graph エクスプローラーに初めてアクセスすると、 **[アクセス許可が要求されました(Permissions requested)]** ページが表示されます。 **[同意する(Accept)]** を選択します。

5. ページの上の方にある **[GET]** ボタンを選択し、ドロップダウンメニューから **[POST]** を選択します。

6. 真ん中のボックスから**v1.0**を変更しないでください。

7. ページの中央上の方にあるテキスト ボックス ([POST]の右]) に次のように入力します。

   - **https://graph.microsoft.com/v1.0/teams**

8. 上部のウィンドウから [**Modify permissions]** を選択します。

   [![Graphical user interface, text, application, email Description automatically generated](https://github.com/MicrosoftLearning/MS-700-Managing-Microsoft-Teams/raw/master/Instructions/Labs/media/MS-700-lab_M03_ak_image1.png)](https://github.com/MicrosoftLearning/MS-700-Managing-Microsoft-Teams/blob/master/Instructions/Labs/media/MS-700-lab_M03_ak_image1.png)

9. 右にスクロールし、アクセス許可 **Team.Create** の **[Consent**] ボタンを選択します。

10. 別の **[アクセス許可が要求されました(Permissions requested)]** ページが表示されます。 **[同意する(Accept)]** を選択します。

11. Microsoft Developers サイトにリダイレクトされた場合は、次の **Graph エクスプローラー**に戻ります https://developer.microsoft.com/graph/graph-explorer

12. [**Request body**] タブを選択し、次のコードを入力します。(ラボ環境に転記時に余計な文字が入ることがあるため、転記方法は講師の指示に従ってください。ラボ内のブラウザーに本手順のURLを転記して開き、ラボ内でコピー＆ペーストする等の手段が考えられます。)

    ```
    {
    
    "template@odata.bind":"https://graph.microsoft.com/v1.0/teamsTemplates('standard')",
    
    "displayName": "Early Adopters",
    
    "description": "The Early Adopters Workspace.",
    
    "visibility": "Public" 
    
    }
    ```

    

13. ページの右上にある **[Run query]**  を選択します。

14. しばらくすると、 [要求本文] ウィンドウの下に緑色のバーが表示され、チェックマークと **[Accepted]** のメッセージが表示されます。

15. **Request body**のテキストボックス内のテキストボックスの内容全体を削除し、チームを作成して次のコンテンツに置き換えます。

    ```
    {
    
    "template@odata.bind": "https://graph.microsoft.com/v1.0/teamsTemplates('standard')",
    
    "visibility": "Public",
    
    "displayName": "Tech Meetings",
    
    "description": "Space for all employees participating in the champions program, who want exchange each other about the newest features.",
    
    "channels": [
    
    {
    
    "displayName": "Welcome Hall",
    
    "isFavoriteByDefault": true,
    
    "description": "Channel for introducing yourself as a member of the tech meeting participants."
    
    },
    
    {
    
    "displayName": "Tech Lunch and Dinner",
    
    "isFavoriteByDefault": true,
    
    "description": "When will be the next tech lunch and who has any suggestions where to meet."
    
    },
    
    {
    
    "displayName": "Q and A",
    
    "description": "Questions and answers: Teams users giving a helping hand to other users.",
    
    "isFavoriteByDefault": true
    
    },
    
    {
    
    "displayName": "Issues and Feedback 🐞",
    
    "description": "Leave some feedback for the IT-Staff.",
    
    "isFavoriteByDefault": false
    
    }
    
    ],
    
    "memberSettings": {
    
    "allowCreateUpdateChannels": true,
    
    "allowDeleteChannels": false,
    
    "allowAddRemoveApps": true,
    
    "allowCreateUpdateRemoveTabs": true,
    
    "allowCreateUpdateRemoveConnectors": true
    
    },
    
    "guestSettings": {
    
    "allowCreateUpdateChannels": true,
    
    "allowDeleteChannels": false
    
    },
    
    "funSettings": {
    
    "allowGiphy": true,
    
    "giphyContentRating": "Moderate",
    
    "allowStickersAndMemes": true,
    
    "allowCustomMemes": true
    
    },
    
    "messagingSettings": {
    
    "allowUserEditMessages": true,
    
    "allowUserDeleteMessages": true,
    
    "allowOwnerDeleteMessages": true,
    
    "allowTeamMentions": true,
    
    "allowChannelMentions": true
    
    },
    
    "discoverySettings": {
    
    "showInTeamsSearchAndSuggestions": true
    
    }
    
    }
    ```

    

16. ページの右上にある **[Run query]** を選択します。

17. しばらくすると、チェックマークが付いた緑色のバーが表示され、再び **[承認済み**] が表示されます。

18. Teams デスクトップ アプリを開き、左側のウィンドウから **[Teams**] を選択し、新しく作成されたチーム "**Early Adopters**" と "**Tech Meetings**" を調べます。

Graph API を使用して 2 つのチームを正常に作成しました。グラフ機能のテストが完了したので、次の演習に進むことができます。

#### タスク 4 – チームのアーカイブとアーカイブ解除

このラボでさまざまなチームを作成したら、チームを削除するさまざまな方法を再度評価する必要もあります。このタスクでは、アーカイブ機能をテストし、営業チームのコンテンツを削除せずに非アクティブ化状態に変更します。この機能は、チーム内で保存されたデータを保持するという一部の企業のコンプライアンス要件に必要です。このタスクに十分な特権を持つ唯一の Teams 管理者ロールは、現在 Joni Sherman に割り当てられている Teams 管理者であるため、このタスクには Joni のアカウントを使用します。

1. **クライアント 1 VM** とブラウザーを Teams 管理センター(https://admin.teams.microsoft.com)に接続し、 Joni Sherman (JoniS@YourTenant.onmicrosoft.com) としてサインインします。
2. 左側のウィンドウから [**チーム**] を選択し、[**チームを管理**] を選択します。
3. Salesチームのアーカイブ
   1. **Sales**チーム左のチェックマークを選択し、ウィンドウ上部のから **アーカイブ** を選択します。
   2. [**SharePoint サイトをチーム メンバーに対して読み取り専用にする**] チェック ボックスをオンにし、[**アーカイブ**] を選択します。
   3. [ステータス] 列が [アーカイブ済み] に変わり、オレンジ色で表示されます。ブラウザを開いたままにして続行します。**Sales**チームに問題がある場合は、別のチームをアーカイブします(このアクションはアーカイブ解除手順で元に戻すことができます)。
4. アーカイブされたチームを確認する
   1. **クライアント 2 VM** に接続し、[**Microsoft Teams Web クライアント (https://teams.microsoft.com/)**](https://teams.microsoft.com/) を Lynne Robbins (LynneR@YourTenant.onmicrosoft.com) として参照します。
   2. **[Teams]**  を選択し、[Teams] の右にある **[...]** を選択して、[**Manage teams**] をクリックします。
   3. **[Archived]** セクションを展開し、[**Sales**] を選択します。
   4. 「This Team was archived, so you can't post any more messages.」と画面下の方に表示され、[Start a post]でメッセージが送信できないことを確認します。
5. Salesチームのアーカイブを解く
   1. **クライアント 1 VM** に再度接続し、**Joni Sherman** として Teams 管理センターを参照します。
   2. **[Sales**] の左側にあるチェックボックスをもう一度選択し、上部のメニューから [**アーカイブを解除**] を選択します。[**状態**] フィールドが再び **[アクティブ**] に変わります。
6. アーカイブされていないチームを確認する
   1. **クライアント 2 VM** に接続し、[**Microsoft Teams Web クライアント (https://teams.microsoft.com/)**](https://teams.microsoft.com/) を **Lynne Robbins** (LynneR@YourTenant.onmicrosoft.com) として参照します。
   2. 左側にある **[Team**] を選択します。
   3. Sales チームと**General** チャネルのテキストはしばらくすると通常に戻りますが、チームは非表示になっています。
   4. Sales チーム名の右にあるから 3 つのドット **(...)** を選択し、**Show** を選択します。
7. ブラウザーを開いたままにして、サインインしたままにします。

チームを正常にアーカイブし、アーカイブされたチームの制限された機能を確認しました。これにより、コンプライアンス保持ポリシーとルールのチームのアーカイブ機能をテストするという最初の要件が満たされます。このテストの後、チームを再びアーカイブ解除し、完全に機能するようになりました。

#### タスク 5 - チームの削除と回復

このタスクでは、前のレッスンで作成したチームの 1 つを削除し、復元する方法を学習します。

1. **クライアント 2 VM** に接続し、[**Microsoft Teams Web クライアント (https://teams.microsoft.com/)**](https://teams.microsoft.com/) を Lynne Robbins (LynneR@YourTenant.onmicrosoft.com) として参照します。
2. Teams Web クライアントの左側のナビゲーション ウィンドウで、**Sales** チームから 3 つのドット (...) を選択し、一覧から **[Delete team]** を選択します。
3. **I understand that everything will be deleted** のチェックボックスをオンにして、 **[Delete team]** を選択します。
4. グループの回復
   1. **クライアント 1 VM** に接続し、**MOD 管理者**として Entra ID 管理センター (https://entra.microsoft.com/) を参照します。
   2. 左側のナビゲーション ウィンドウで、[**ID** > **グループ** > **削除したグループ**] を選択します。
   4. これで、**Sales** グループを含むすべての削除されたグループが表示されます。
   5. **Sales** グループの左側にあるチェック ボックスをオンにし、ウィンドウ上部の [**グループの復元**] ボタンを選択します。[削除済みのグループを復元しますか] ダイアログで **[はい**] を選択して確認します。
5. 復元されたグループを確認します。
   1. **クライアント 2 VM** に接続し、[**Microsoft Teams Web クライアント (https://teams.microsoft.com/**](https://teams.microsoft.com/)) を **Lynne Robbins** (LynneR@YourTenant.onmicrosoft.com) として参照します。
   2. **Sales** チームがチームの一覧に再び表示されます。必要に応じて、**F5** キーを押してページを更新します。
   3. チーム名から 3 つのドット (...) を選択し、[**Manage teams**] を選択します。所有者とすべてのメンバーを [**メンバー**] タブで再度確認できます。

**手記：** チームの削除と復元の完全なプロセスには、最大で 24 時間かかる場合があります。再度表示されない場合は、このラボの後で確認してください。

Teams Web クライアントを使用してチームを正常に削除し、Azure Portal で復元しました。

#### タスク 6 - 動的メンバーシップでチーム メンバーを管理する

Contoso はカナダに進出し、トロントに新しいオフィスを開設します。システム管理者は、Office 365 サービスの場所に基づいてメンバーシップを持つ動的グループを構成する必要があります。

1. **クライアント 1 VM** に接続し、**MOD 管理者**として Entra ID 管理センター (https://entra.microsoft.com/) を参照します。

2. 左側のナビゲーション ウィンドウで、[**ID** > **グループ** > **すべてのグループ**] を選択します。

3. グループ |すべてのグループ ページで、**CA-Office** グループを検索して選択します。

4. **[CA-Office**] ページで、左側のナビゲーションから [**プロパティ**] を選択します。

5. **[メンバーシップの種類**] を [**割り当て済み**] から **[動的ユーザー**] に変更します。

6. **[動的ユーザー メンバー**] の下にある [**動的クエリの追加]** を選択します。

7. [**動的メンバーシップ ルール**] ページで、フィールドに次の情報を入力します。

   - プロパティ: **accountEnabled**
   - 演算子: **Equals**
   - 値: **true**

8. **[+ 式の追加**] を選択し、フィールドに次の情報を入力します。

   - プロパティ: **usageLocation**
   - 演算子: **Equals**
   - 値: **CA**

9. [**保存**] を 2 回選択します。

   メンバーシップが新しい動的メンバーシップ規則に従って変更されることを示す警告メッセージが表示されます。[**はい**] を選択してメッセージを確認します。

10. **CA-Office** グループ ウィンドウの左側のナビゲーション ウィンドウで [**概要**] を選択します。

11. 「概要」ウィンドウで、「**動的ルール処理状態**」フィールドを見つけます。

    ステータスが **[成功]** と表示されるまで、ブラウザーを更新して待機します。変更が処理されるまでに数分かかる場合があります。

12. 次に、左側のナビゲーション ウィンドウで [**メンバー**] を選択し、 [**最新の情報に更新]** を選択します。**Alex Wilber** がメンバーのリストに含まれているが、**Allan Deyoung** がグループから削除されていることを確認します。

13. 左側のナビゲーション ウィンドウから [所有者] を選択し、Joni が動的グループの条件に一致しない場合でも、グループの所有者であることを確認します。

Microsoft 365 グループを静的 (割り当て済み) から動的メンバーシップに正常に変換しました。このメンバーシップは、ユーザーの usageLocation と、アカウントが有効になっているかどうかによって制御されます。usageLocation が "Canada" のユーザーは、自動的にチームに追加されます。

### 

### **演習 2: チャネル ポリシーとメッセージ ポリシーを構成する**

この演習では、新しいプライベート チャネルの作成と、チャットでユーザーが使用できるツールを管理するポリシーを構成します。

#### タスク 1 - giphy、ミーム、ステッカーのメッセージング ポリシーを作成する

会社は、Teams 通信でのグラフィック要素の使用を制限したいと考えています。Teams サービス管理者は、パイロット ユーザーが Teams チャットとチャネルの会話で GIF ファイル、ミーム、ステッカーを使用することを禁止する新しいメッセージ ポリシーを作成します。

1. **クライアント 1 VM** に接続し、**Joni Sherman** (JoniS@YourTenant.onmicrosoft.com) として Teams 管理センター ([https://admin.teams.microsoft.com](https://admin.teams.microsoft.com/)) を参照します。

2. Teams 管理センターの左側のナビゲーションで、左側のナビゲーションで **[メッセージング]** > [**メッセージング ポリシー**] を選択します。

3. **[ポリシーの管理**] タブで **[+ 追加**] を選択し、次のように入力します

   - **名前**:楽しいもののない常連ユーザー
   - **説明**:会話でgiphys、ステッカー、ミームを無効にするポリシー
   - **会話でのGiphy** :オフ
   - **会議でミーム**:オフ
   - **会話での**ステッカー: オフ
   - 残りの設定はデフォルトのままにします。[**保存**] を選択します。

4. **[メッセージング ポリシー**の概要] ページに戻り、[**楽しいもののない常連ユーザー**] の左側にあるチェックマークを選択します。次に、 **[ユーザーを管理] > [ユーザーの割り当て]** を選択します

   **注**: **[ユーザーの割り当て**] が表示されない場合は、[**ユーザーの管理**] を選択してメニューを展開します。

5. 次のパイロット ユーザーを検索して [**追加**] を選択します。次に、プロンプトが表示されたら [**適用**] と **[確認]** を選択します。

   - **Alex Wilber**
   - **Lynne Robbins**
   - **Diego Siciliani**

**注**: 設定が有効になるまでには、最長で 24 時間ほどかかることがあります。

このタスクでは、新しいメッセージング・ポリシーを正常に構成し、パイロット・ユーザーに割り当てました。今後、ポリシーが有効になるまでに時間がかかります。次のタスクに進みます。

#### タスク 2 - チーム内のプライベート チャネルを管理する

Contoso の Teams 管理者は、一部のチーム メンバーのみがアクセスできる **confidential** という名前のプライベート チャネルを営業チームに作成します。

1. **クライアント 1 VM** に接続し、**Joni Sherman** (JoniS@YourTenant.onmicrosoft.com) として Teams 管理センター ([https://admin.teams.microsoft.com](https://admin.teams.microsoft.com/)) を参照します。
2. Teams 管理センターの左側のナビゲーションで、[**チーム**] > **[チームを管理**] を選択します。
3.  **Sales**チーム を選択します。
4.  **チャネル** タブを選択します。
5. プライベート チャネルを追加する
   1.  **[+ 追加**] を選択します。
   2. 「**追加**」ウィンドウで、次の情報を入力します。
      - **名前**: Confidential sales
      - **説明:** 機密のプライベート販売チャネル
      - **種類**: プライベート
      - **チャンネル所有者**: Lynne Robbins
6. [**適用]** を選択します。
7. プライベートチャネルを確認する
   1. **クライアント 2 VM** に接続し、**Lynne Robbins** (LynneR@YourTenant.onmicrosoft.com) として **Teams Web クライアント** [(https://teams.microsoft.com)](https://teams.microsoft.com/) を参照します。
   2. **[チーム**] を選択すると、小さな南京錠のアイコンが付いた新しいプライベート チャネル [**Confidential sales**] が表示されます。

このタスクでは、Microsoft Teams 管理センターでプライベート チャネルを作成する方法と、アクセスを構成および確認する方法について説明しました。

### **演習 3: アプリの設定を管理する**

#### タスク 1 - サード・パーティー・ストレージ・プロバイダーの無効化

これまで、ユーザーはサードパーティのストレージプロバイダーを含むさまざまな場所にデータを保存していました。最近、同社はすべてのユーザーにOneDriveを導入し、すべてのファイルコラボレーションの代替手段としてBoxを使用して、SharePointとOneDriveを主要なデータストレージの場所として使用するようにユーザーをガイドしたいと考えています。Teams 管理者は、方向に合わせて、Microsoft Teams の Box を除くすべてのサードパーティ ストレージ プロバイダーを非アクティブ化するように求められます。

1. **クライアント 1 VM** に接続し、**Joni Sherman** (JoniS@YourTenant.onmicrosoft.com) として Teams 管理センター ([https://admin.teams.microsoft.com](https://admin.teams.microsoft.com/)) を参照します。
2. Teams 管理センターの左側のナビゲーションで、[チーム] > **[Teams の設定**] を選択します。
3. **[Teams の設定**] ページで、[**ファイル**] セクションに移動します。
4. 次のファイル共有とクラウドファイルストレージのオプションを設定します。
   -  **Citrix files:** オフ
   -  **DropBox:** オフ
   -  **Box：** オン
   -  **Googleドライブ:** オフ
   -  **Egnyte:** オフ
5. 下にスクロールして [**保存**] を選択します。

**注**: 設定が有効になるまでには、最長で 24 時間ほどかかることがあります。

このタスクでは、テナント全体に対してサードパーティのストレージプロバイダーを有効または無効にする方法を学習しました。

#### タスク 2 - 組織レベルでアプリをブロックする

このタスクでは、すべてのテナントに対して Google アナリティクス アプリをブロックします

1. **クライアント 1 VM** に接続し、**Joni Sherman** (JoniS@YourTenant.onmicrosoft.com) として Teams 管理センター ([https://admin.teams.microsoft.com](https://admin.teams.microsoft.com/)) を参照します。

2. Teams 管理センターの左側のナビゲーションで、[**Teams のアプリ**] > [**アプリを管理**] を選択します。

3. [**アプリの管理**] ページで、検索ボックスに「**Google**」と入力します。

   [![Graphical user interface, application Description automatically generated](https://github.com/MicrosoftLearning/MS-700-Managing-Microsoft-Teams/raw/master/Instructions/Labs/media/MS-700-lab_M03_ak_image5.png)](https://github.com/MicrosoftLearning/MS-700-Managing-Microsoft-Teams/blob/master/Instructions/Labs/media/MS-700-lab_M03_ak_image5.png)

4. 検索結果で **[Google Analytics]** を選択して開きます。

5. 画面右上の **[アクション]** を選択します。

6. [**アプリをブロック]** を選択します。

**注**: 設定が有効になるまでには、最長で 24 時間ほどかかることがあります。

このタスクでは、テナントの Google アナリティクス アプリをブロックする方法を学習しました。

### **演習 4: アプリのセットアップ ポリシーを作成および管理する**

Teams 管理者は、ユーザーにとって最も重要なアプリを強調し、組織内のユーザーが必要とするアプリ (サード パーティ、パーティ、または組織内の開発者によって構築されたアプリを含む) も紹介する必要があります。

#### タスク 1 - 既定の組織全体のアプリ ポリシーを編集する

パイロット プロジェクトでは、**Planner と To Do によるタスク**をすべてのユーザーの既定のアプリとして追加したいと考えています。これを行うには、既定の組織全体のアプリ ポリシーを編集します。このタスクは、テナント全体に伝達されるまでに時間がかかる場合があります。

1. **クライアント 1 VM** に接続し、**Joni Sherman** (JoniS@YourTenant.onmicrosoft.com) として Teams 管理センター ([https://admin.teams.microsoft.com](https://admin.teams.microsoft.com/)) を参照します。
2. Teams 管理センターの左側のナビゲーションで、[**Teamsの アプリ**] > [**セットアップ ポリシー**] を選択します。
3. [**アプリのセットアップ ポリシー**] ページの [ポリシーの管理] で、 **[グローバル (組織全体の既定値)]** を選択して、組織全体のアプリ ポリシーを開きます。
4. [**ピン留めされたアプリ**] セクションで、[**アプリを追加**] を選択します。
5. [**インストール済みアプリを追加**] ページで、検索ボックスに **「Planner および To Do タスク」** と入力し、名前の上にマウスを合わせて [**追加**] を 2 回選択します。
6. **[Planner および To Do タスク**] が [**ピン留めされたアプリ**] セクションに一覧表示されていることを確認し、**[保存]** して **[確認]** を選択します。

**注**: 設定が有効になるまでには、最長で 24 時間ほどかかることがあります。

このタスクでは、Microsoft Teams 管理センターから既定のアプリをピン留めする方法について説明しました。

#### タスク 2 - カスタム アプリ設定ポリシーを作成するTask 2 - Create a custom app setup policy

1. **クライアント 1 VM** に接続し、**Joni Sherman** ([**JoniS@.onmicrosoft.com**](mailto:JoniS@.onmicrosoft.com)) として Teams 管理センター (**[https://admin.teams.microsoft.com](https://admin.teams.microsoft.com/)**) を参照します。

2. Microsoft Teams管理センターの左側のナビゲーションで、[**Teams アプリ**] > [**セットアップ ポリシー**] に移動します。

3. [**+** **追加**] を選択します。

4. 次の情報を入力します

   - 名前: **Salesチーム**

   - 説明: **Adobe Acrobat Sign をインストールし、Viva ゴールをピン留めします。**

   - ユーザーのピン留め: **オン**

   - ユーザー用のアプリをインストールするには:

     1. **[インストール済みアプリ**] で [**アプリを追加**] を選択します。

     2. [**インストール済みアプリの追加**] ウィンドウで、ユーザーが Teams を起動したときに自動的にインストールするアプリを検索します。

        この演習では、「Adobe」を検索し、「**Adobe Acrobat Sign**」を選択し、**「追加」** を選択して「追加するアプリ」リストに追加します。

        これで、 [**追加]** を選択して、 **[インストール済みアプリの一覧] でアプリ**の追加を完了できます。

   - アプリをピン留めするには:

     1. [**ピン留めされたアプリ**] で [**アプリを追加**] を選択します。
     2. [**ピン留めされたアプリの追加**] ウィンドウで、[**Viva Goals**] を検索し、[**追加**] を選択します。
     3. [**保存**] を選択します。

5. [**保存**] を選択します。

これで、新しいカスタム アプリ設定ポリシーが作成されました。

#### タスク 3 - カスタム アプリ設定ポリシーをユーザーに割り当てる

1. **Microsoft Teams管理センターの**左側のナビゲーション ウィンドウで、[**Teams のアプリ**] > [**セットアップ ポリシー**] に移動します。
2. **Salesチーム** のアプリ設定ポリシー の左のチェックをオンにします。
3. **[ユーザーを管理] - [ユーザーの割り当て]** を選択します。
4. [**ユーザーを管理**] ウィンドウで、**Alex Wilber** を検索し、[**追加**] を選択します。
5. [**適用]** および **[確認]** を選択します。

### **演習 5: 構成済みのポリシー設定をテストする**

この演習では、影響を受けるユーザー **Lynne Robbins** を使用してクライアントで構成されたポリシー設定をテストし、その設定を **Joni Sherman** の使用可能なクライアント設定と比較します。

#### タスク 1 – メッセージング ポリシーとプライベート チャネル アクセスをテストする

このタスクでは、演習 1 で構成された**メッセージング ポリシー**をテストし、影響を受けるユーザー (Lynne Robbins) と通常のユーザー (Joni Sherman) の違いを比較します。

1. **クライアント 2 VM** に接続し、[**Microsoft Teams Web クライアント (https://teams.microsoft.com/**](https://teams.microsoft.com/)) を **Lynne Robbins** (LynneR@YourTenant.onmicrosoft.com) として参照します。

2. 左側のナビゲーション ウィンドウで、[**Chat**] > **[New chat]** アイコンを選択します。

   [![Graphical user interface, application Description automatically generated with medium confidence](https://github.com/MicrosoftLearning/MS-700-Managing-Microsoft-Teams/raw/master/Instructions/Labs/media/MS-700-lab_M03_ak_image8.png)](https://github.com/MicrosoftLearning/MS-700-Managing-Microsoft-Teams/blob/master/Instructions/Labs/media/MS-700-lab_M03_ak_image8.png)

3. メイン ウィンドウで、「**Joni Sherman**」と入力して会話を開始します。

4. **giphy**、**ミーム**、**ステッカー**のアイコンがないことに注意してください。

#### タスク 2 – ブロックされたアプリとストレージ プロバイダーをテストする

このタスクでは、ブロックされたアプリをテストします。

1. **クライアント 2 VM** に接続し、[**Microsoft Teams Web クライアント (https://teams.microsoft.com/**](https://teams.microsoft.com/)) を **Lynne Robbins** (LynneR@YourTenant.onmicrosoft.com) として参照します。
2. 左側のナビゲーションで **[Apps**] を選択します。
3. 検索ボックスから**Google**を検索します。
4. 検索結果で **[Google Analytics]** を選択します。ロックアイコンと「リクエスト」ボタンに注意してください。
5. 左側のナビゲーション ウィンドウで、**Teams** を選択し、**Sales**チームの **General** チャネルに移動します。
6. **[FIles]** タブを選択し、[**Share**] アイコンを選択します
7. [**Copy link**] を選択します
8. オプションとして SharePoint と Box のみが表示され、Teams 設定のクラウド ファイル ストレージ設定が期待どおりに機能したことに注意してください。
9. Teams からサインアウトし、開いているウィンドウをすべて閉じます。

ラボ終了
