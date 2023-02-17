# replace_real-estate_kanri

## repository

```
app/
  └ components/
      ├─ pages/ #1
      │     ├─ index/
      │     │     └─ TheLoginForm
      │     ├─ reset_password/
      │     │     └─ TheResetForm
      │     ├─ change_password/
      │     │     └─ TheChangeForm  
      |     ├─ admin/
      │     │     └─ .gitkeep
      │     ├─ company/
      │     │     └─ edit/
      │     │         └─ UpdateCompany
      │     ├─ list/
      │     │     └─ id/
      │     │         └─ UpdateMemo
      │     ├─ setting/
      │     │     ├─ ChangeTab
      │     │     ├─ UpdateDeliveryCities
      │     │     ├─ UpdateDeliveryTowns
      │     │     ├─ UpdateDeliveryPropertyType
      │     │     └─ UpdateDeliveryPropertyCondition
      │     └─ result/
      │           ├─ index/
      │           │     └─ .gitkeep
      │           ├─ property_type_select/
      │           │     └─ SelectPropertyType
      │           ├─ input/
      │           │     └─ TheRegistForm
      │           ├─ convert/
      │           │     └─ TheConvertToCsv
      │           └─ csv_import
      │                 └─ TheImportCsv
      ├─ projects/ #2
      │     ├─ TheHeader
      │     ├─ TheFooter
      │     ├─ TheGlobalNavigation
      │     ├─ OrderSearch
      │     └─ SalesResultSearch
      └ parts/ #3
            ├─ BaseLogo
            ├─ BaseButton
            ├─ BasePageTitle
            ├─ BaseTable
            ├─ BaseModal
            ├─ SalesContact
            ├─ DeliveryRadioButton
            ├─ DeliveryCheckbox
            ├─ DeliverySettingList
            ├─ OrderTerms
            ├─ OrderTable
            ├─ SalesResultTerms
            ├─ SalesResultTable
            ├─ PageNation
            ├─ SelectPrefModal
            ├─ SelectRailModal
            ├─ SelectStationModal
            ├─ SelectCityModal
            ├─ SelectTownModal
            └─ BatchRegistHeader
            
            
```

#1 そのページのみで使用する機能を持ったコンポーネント  
#2 ページをまたいで使用される機能を持ったコンポーネント  
#3 propsやslotで表示を変えたり、emitで親コンポーネントに値を送るコンポーネント、または要素を表示するだけのコンポーネント（store, route, API等の使用も禁止）  

### なぜこの構成にしようとしたのか？
- 可読性、可変性、保守性の観点から品質を高めるため
- 状態管理をapp/pages/で管理してもstateのバケツリレーの階層が2階層以上にならないpages ⇔ component ⇔ parts
- ページ単体なのか複数のページにまたがるのかで影響範囲がわかりやすい

## rules
- app/pages/では極力ファイル名によるディレクトリ管理を行わない  
  下層ページができる際にディレクトリの作成や既存ページのファイルパスなどの変更が発生してしまうため
- ページをまたいで共通の変数を使用する場合plugins/variables/に定義しnamed exportをする
- ファイルの命名ルールにはこちらの推奨を参考にする(https://ja.vuejs.org/style-guide/)  

## pages
### /index
#### 機能
- ログイン機能

#### 使用コンポーネント
- pages/index/TheLoginForm
- parts/BaseLogo
- parts/BaseButton
- parts/SalesContact

### /reset_password
#### 機能
- パスワード再設定のメールを送信

#### 使用コンポーネント
- pages/reset_password/TheResetForm
- parts/BaseLogo
- parts/BaseButton
- parts/SalesContact

### /change_password
#### 機能
- パスワードの変更

#### 使用コンポーネント
- pages/change_password/TheChangeForm
- parts/BasePageTitle
- parts/BaseButton

### /setting
#### 機能
- 配信地域を更新(市区町村)
- 配信地域を更新(町域)
- 配信する物件種別を更新
- 配信する物件の詳細を更新

#### 使用コンポーネント
- pages/setting/ChangeTab
- pages/setting/UpdateDeliveryCities
- pages/setting/UpdateDeliveryTowns
- pages/setting/UpdateDeliveryPropertyType
- pages/setting/UpdateDeliveryPropertyCondition
- parts/DeliveryRadioButton
- parts/DeliveryCheckbox
- parts/DeliverySettingList
- parts/BaseButton

### /list
#### 機能
- 案件を検索

#### 使用コンポーネント
- projects/OrderSearch
- parts/OrderTerms
- parts/PageNation
- parts/OrderTable
- parts/BasePageTitle

### /list/:id
#### 機能
- メモを更新する  
  ※印刷はwindow.printで実装するため特に機能として実装しない

#### 使用コンポーネント
- pages/list/id/UpdateMemo
- parts/BasePageTitle
- parts/BaseButton
- parts/ModalDefault
- parts/BaseTable

### /company
#### 機能
なし

### 使用コンポーネント
- parts/BasePageTitle
- parts/BaseTable

### /company/edit
#### 機能
- 会社情報、各種設定更新

#### 使用コンポーネント
- pages/company/edit/TheUpdateCompany
- parts/BasePageTitle
- parts/BaseTable
- parts/BaseButton

### /result
#### 機能
- 売却実績を検索
- 売却実績を公開非公開の切り替え
- 売却実績を削除

#### 使用コンポーネント
- projects/SalesResultSearch
- projects/SalesResultTerms
- projects/SalesResultTable
- parts/PageNation
- parts/SalesResultNavigation

### /result/property_type_select
#### 機能
- 物件種別を選択し遷移先の/result/inputで選択した物件種別を利用可能にする(store)

#### 使用コンポーネント
- pages/result/property_type_select/SelectPropertyType
- parts/SalesResultNavigation

### /result/input
#### 機能
- 入力したデータで売却実績を登録できる機能

#### 使用コンポーネント
- parts/SalesResultNavigation
- parts/SelectPrefModal
- parts/SelectRailModal
- parts/SelectStationModal
- parts/SelectCityModal
- parts/SelectTownModal

### /result/convert
#### 機能
- txtファイルを選択しcsvファイルに変換する

#### 使用コンポーネント
- pages/result/convert/TheConvertToCsv
- parts/SalesResultNavigation
- parts/BasePageTitle
- parts/BatchRegistHeader

### /result/csv_import
#### 機能
- csvファイルを選択しインポートを実行する

#### 使用するコンポーネント
- pages/result/csv_import/TheImportCsv
- parts/SalesResultNavigation
- parts/BasePageTitle
- parts/BatchRegistHeader

### /admin/
#### 機能
- 案件を検索
- テーブルをcsvでダウンロード

#### 使用コンポーネント
- projects/OrderSearch
- parts/OrderTerms
- parts/PageNation
- parts/OrderTable
- parts/BasePageTitle

### /admin/result
#### 機能
- 売却実績を検索

#### 仕様コンポーネント
- projects/SalesResultSearch
- projects/SalesResultTerms
- projects/SalesResultTable
- parts/PageNation


## 相談
- BaseButtonの有用性が分からない。ただのstyleの為のものならscssのmixinで十分では？その方が可変性もあるのでは？  
→ styleの種類が少ないのでmixinにする
- APIはpluginsにまとめて必要なものをnamed exportで呼び出す形が良いか  
→ まとめることを推奨されているがビルドサイズ次第 named export調べる
- 初期表示に必要なAPIの実行は基本的にpages側で行い、機能に関係するAPIについてはcomponentのpages, projectsのみ許容とか？  
これでよい
- ↑の追加で、ものによってはcomponentで実行するAPIとほかのコンポーネントだが同じAPIを実行したいことがある場合はpagesにAPIのparam管理とAPI実行を任せた方がいい場合もある(/result/の検索機能とページ変更)
→ その時次第で使い分けでよい
- バケツリレーが2階層以内である強みを生かすのであればAPIはすべてpagesの実行でも大変ではないのでは？  
→ 上と同じ

## 参考にしたもの
- https://note.com/tabelog_frontend/n/n07b4077f5cf3
- https://zenn.dev/offers/articles/20220523-component-design-best-practice
- https://zenn.dev/morinokami/books/learning-patterns-1/viewer/presentational-container-pattern



