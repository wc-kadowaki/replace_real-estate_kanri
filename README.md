# replace_real-estate_kanri

## repository

```
app/
  └ components/
      ├─ pages/ #1
      │     ├─ index/
      │     │     └─ TheLoginForm.vue
      │     ├─ reset_password/
      │     │     └─ TheResetForm.vue
      │     ├─ change_password/
      │     │     └─ TheChangeForm.vue
      │     ├─ setting/
      │     │     ├─ UpdateDeliveryCities
      │     │     ├─ UpdateDeliveryTowns
      │     │     ├─ UpdateDeliveryPropertyType
      │     │     └─ UpdateDeliveryCondition
      |     ├─ admin/
      │     │     └─ .gitkeep
      │     ├─ company/
      │     │     └─ edit/
      │     │         └─ UpdateCompany
      │     ├─ list/
      │     │     └─ id/
      │     │         └─ UpdateMemo
      │     ├─ setting/
      │     │     ├─ UpdatePropertyTypeCondition.vue
      │     │     ├─ UpdateDeliveryArea.vue
      │     │     └─ UpdateDeliveryConditionModal.vue
      │     └─ result/
      │           ├─ index/
      │           │     └─ .gitkeep
      │           ├─ property_type_select/
      │           │     └─ .gitkeep
      │           ├─ input/
      │           │     └─ Regist
      │           ├─ convert/
      │           └─ csv_import
      ├─ projects/ #2
      │     ├─ TheHeader.vue
      │     ├─ TheFooter.vue
      │     ├─ TheGlobalNavigation.vue
      │     ├─ OrderSearch
      │     └─ 
      └ parts/ #3
            ├─ BaseLogo.vue
            ├─ BaseButton.vue
            ├─ BasePageTitle.vue
            ├─ SalesContact.vue
            ├─ DeliveryRadioButton
            ├─ DeliveryCheckbox
            ├─ DeliverySettingList
            ├─ TabPanel.vue
            ├─ OrderTerms
            ├─ OrderTable
            ├─ ModalDefault
            
            
```

#1 そのページのみで使用する機能を持ったコンポーネント（単一の機能の場合parts）  
#2 ページをまたいで使用される機能を持ったコンポーネント（単一の機能の場合parts）  
#3 単一の機能を持つまたは機能を持たないコンポーネント（storeへのアクセス及びAPIの使用も禁止）

### なぜこの構成にしようとしたのか？
- 状態管理をapp/pages/で管理してもstateのバケツリレーの階層が2階層以上にならない
- ページ単体なのか複数のページにまたがるのかで影響範囲がわかりやすい

## rules
- app/pages/では極力ファイル名によるディレクトリ管理を行わない  
  下層ページができる際にディレクトリの作成や既存ページのファイルパスなどの変更が発生してしまうため
- ページをまたいで共通の変数を使用する場合plugins/variables/に定義しnamed exportをする
- ファイルの命名ルールにはこちらの推奨を用いる(https://ja.vuejs.org/style-guide/)  

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
- pages/setting/TabPanel
- pages/setting/UpdatePropertyTypeCondition
- pages/setting/UpdateDeliveryArea
- pages/setting/UpdateDeliveryConditionModal
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

### /company
#### 機能
なし

### 使用コンポーネント
- parts/BasePageTitle

### /company/edit
#### 機能
- 会社情報、各種設定更新

#### 使用コンポーネント
- pages/company/edit/TheUpdateCompany
- parts/BaseButton

### /result
#### 機能
- 売却実績を検索

#### 使用コンポーネント
- projects/SalesResultSearch
- projects/SalesResultTerms
- projects/SalesResultTable
- projects/PageNation
- parts/SalesResultNavigation

### /result/property_type_select
#### 機能
- 物件種別を選択し遷移先の/result/inputで選択した物件種別を利用可能にする(store)

#### 使用コンポーネント
- なし

### /result/input
#### 機能
- 入力したデータで売却実績を登録できる機能

#### 使用コンポーネント


## 相談
- BaseButtonの有用性が分からない。ただのstyleの為のものならscssのmixinで十分では？その方が拡張性もあるのでは？
- APIはpluginsにまとめて必要なものをnamed exportで呼び出す形が良いか
- company/editの特徴選択はコンポーネントにするべきか？  
  特徴選択（サービス、スタッフ）、諸々の設定の3つのコンポーネントから値をpagesで受け取りpagesでAPI実行みたいなイメージならコンポーネントにするべきだがコンポーネントにどこまでの責任を持たせるべきか？
- APIの実行はコンポーネント側で行うかpages側で行うのか？
- APIの実行は基本的にpages側で行い、表示や選択しに関わるAPIのgetについてはcomponentのpages, projectsのみ許容とか？
