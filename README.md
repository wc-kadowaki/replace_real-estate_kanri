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
      │     │     ├─ TabPanel.vue
      │     │     ├─ PrefSelect.vue
      │     │     ├─ CitySelect.vue
      │     │     ├─ DeliveryAreaUpdate.vue
      │     │     ├─ DeliveryAreaList.vue
      │     │     ├─ DeliveryCityModal.vue
      │     │     ├─ PropertyTypeSelect.vue
      │     │     ├─ PropertyTypeConditionUpdate.vue
      │     │     ├─ DeliveryPropertyTypeList.vue
      │     │     └─ DeliveryPropertyTypeModal.vue
      │     └─ result/
      │           ├─ index/
      │           │     └─ .gitkeep
      │           ├─ property_type_select/
      │           │     └─ .gitkeep
      │           ├─ input/
      │           ├─ convert/
      │           └─ csv_import
      ├─ projects/ #2
      │     ├─ TheHeader.vue
      │     ├─ TheFooter.vue
      │     ├─ TheGlobalNavigation.vue
      │     ├─ OrderSearch
      │     └─ OrderTable.vue
      └ parts/ #3
            ├─ BaseLogo.vue
            ├─ BaseInput.vue
            ├─ BaseInputRadioButton
            ├─ BaseInputDate
            ├─ BaseButton.vue
            ├─ BaseSalesContact.vue
            ├─ BasePageTitle.vue
            ├─ BaseTabNavigation
            ├─ BaseDeliveryRadioButton
            ├─ BaseDeliveryCheckbox
            ├─ BaseDeliverySettingList
            ├─ BaseDeliverySettingList
            ├─ BaseOrderTerms
            ├─ BaseOrderTable
            ├─ BaseModal
            
            
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
- ファイルの命名ルールにはvuejs公式の推奨を用いる  
  単一インスタンスのコンポーネント名には接頭辞として「The」を付ける
  基底コンポーネントの名前には接頭辞として「Base」を付ける

## pages
### /index
#### 機能
- ログイン機能

#### 使用コンポーネント
- pages/index/TheLoginForm
- parts/BaseLogo
- parts/BaseInput
- parts/BaseButton
- parts/BaseSalesContact

### /reset_password
#### 機能
- パスワード再設定のメールを送信

#### 使用コンポーネント
- pages/reset_password/TheResetForm
- parts/BaseLogo
- parts/BaseButton
- parts/BaseSalesContact

### /change_password
#### 機能
- パスワードの変更

#### 使用コンポーネント
- pages/change_password/TheChangeForm
- parts/BasePageTitle
- parts/BaseInput
- parts/BaseButton

### /setting
#### 機能
- 配信地域を更新(市区町村)
- 配信地域を更新(町域)
- 配信する物件種別を更新
- 配信する物件の詳細を更新

#### 使用コンポーネント
- pages/setting/TheUpdateDeliveryCities
- pages/setting/TheUpdateDeliveryTowns
- pages/setting/TheUpdateDeliveryPropertyType
- pages/setting/TheUpdateDeliveryCondition
- parts/BaseTabNavigation
- parts/BaseDeliveryRadioButton
- parts/BaseDeliveryCheckbox
- parts/BaseButton
- parts/BaseDeliverySettingList
- parts/BaseModal

### /list
#### 機能
- 案件を検索

#### 使用コンポーネント
- projects/TheOrderSearch
- parts/BaseOrderTerms
- parts/BaseOrderTable
- parts/BasePageTitle
- parts/BaseInput
- parts/BaseInputRadioButton
- parts/BaseInputDate

### /list/:id
#### 機能
- メモを更新する
- 印刷はwindow.printで実装するため特に機能として実装しない

#### 使用コンポーネント
- pages/list/id/TheUpdateMemo
- parts/BasePageTitle
- parts/BaseButton
- parts/BaseModal

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
- parts/BaseInput
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
- parts/BaseInput
- parts/BaseInputRadioButton
- parts/BaseInputDate






## 相談
- BaseInputは不要では？属性による拡張が大変なのでコンポーネントにしない方がいいのでは？ただのstyleの為のものならscssのmixinで十分
- ↑の理由ならBaseButtonも不要
- APIの実行はコンポーネント側で行うかpages側で行うのか？
- APIはpluginsにまとめて必要なものをnamed exportで呼び出す形が良いか
- 
