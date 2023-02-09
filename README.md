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
      │     │     ├─
      |     ├─ admin/
      │     │     └─ .gitkeep
      │     ├─ company/
      │     │     ├─ InfomationTable.vue
      │     │     └─ featureItemCounter.vue
      │     ├─ list/
      │     │     └─ .gitkeep
      │     └─ setting/
      │           ├─ TheTabPanel.vue
      │           ├─ PrefSelect.vue
      │           ├─ CitySelect.vue
      │           ├─ TheDeliveryAreaUpdate.vue
      │           ├─ DeliveryAreaList.vue
      │           ├─ DeliveryCityModal.vue
      │           ├─ PropertyTypeSelect.vue
      │           ├─ PropertyTypeConditionUpdate.vue
      │           ├─ DeliveryPropertyTypeList.vue
      │           └─ DeliveryPropertyTypeModal.vue
      ├─ projects/ #2
      │     ├─ TheHeader.vue
      │     ├─ TheFooter.vue
      │     ├─ SearchOrder.vue
      │     └─ OrderTable.vue
      └ parts/ #3
            ├─ BaseLogo.vue
            ├─ BaseInput.vue
            ├─ BaseButton.vue
            ├─ BaseSalesContact.vue
            ├─ BasePageTitle.vue
            
            
            
            
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
  pages、projectsには複数単語またはTheが接頭辞としてついているファイルが並び、partsにはBaseの接頭辞がついたファイルが並ぶ

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
- parts/BaseInput
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
- projects/TheUpdateMemo
- parts/BasePageTitle
- parts/BaseButton
- parts/BaseModal






