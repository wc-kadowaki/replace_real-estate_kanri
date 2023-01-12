# replace_real-estate_kanri

## repository
app/
  └ components/
      ├─ pages/ #1
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
            ├─ BaseButton.vue
            ├─ BaseLogo.vue
            ├─ BasePageTitle.vue
            └─ BaseCheckBox.vue
    
#1 そのページのみで使用する機能を持ったコンポーネント（単一の機能の場合parts）
#2 ページをまたいで使用される機能を持ったコンポーネント（単一の機能の場合parts）
#3 単一の機能を持つまたは機能を持たないコンポーネント（storeへのアクセス及びAPIの使用も禁止）

### なぜこの構成にしようとしたのか？
- 状態管理をapp/pages/で管理してもstateのバケツリレーの階層が2階層以上にならない
- ページ単体なのか複数のページにまたがるのかで影響範囲がわかりやすい

## rules
- app/pages/では極力ファイル名によるディレクトリ管理を行わない
  下層ページができる際にディレクトリの作成や既存ページのファイルパスなどの変更が発生してしまうため
- ページをまたいで共通の値を使用する場合plugins/variables/に定義しnamed exportをする
- ファイルの命名ルールにはvuejs公式の推奨を用いる
  pages、projectsには複数単語またはTheが接頭辞としてついているファイルが並び、partsにはBaseの接頭辞がついたファイルが並ぶ
  
