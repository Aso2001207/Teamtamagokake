```uml
@startuml

!define MASTER_MARK_COLOR Orange
!define TEBUE_MARK_COLOR RED
!define TRANSACTION_MARK_COLOR DeepSkyBlue

'グラデーションさせる場合 #xx-xx
!define MAIN_ENTITY #MintCream-MistyRose

/'
  デフォルト色を"skinparam class"で設定します。
'/
skinparam class {
    '図の背景
    BackgroundColor Snow
    '図の枠
    BorderColor Black
    'リレーションの色
    ArrowColor Black
}

package "bookサイト" as target_system {


 entity "購入テーブル" as d_purchase <d_purchase> <<T,TEBUE_MARK_COLOR>>{
+ order_id[PK][NN]
--
customer_id
purchase_date
total_price

}


entity "購入詳細テーブル" as d_purchase_detail <d_purchase_detail> <<T,TEBUE_MARK_COLOR>>{
+ detail_id[PK][NN]
--
order_id
item_name
item_code
price
num

}



entity "顧客マスタ" as m_customers <m_customers> <<M,MASTER_MARK_COLOR>>{
+ customaer_id [PK][NN]
+ pass[PK][NN]
--
name
adress
tel
mail
del_flag
reg_date

}


entity "カテゴリマスタ" as m_category <m_category> <<M,MASTER_MARK_COLOR>>{
+ category_id[PK][NN]
--
name
reg_date

}

entity "お気に入りマスタ" as m_favorite <m_category> <<M,MASTER_MARK_COLOR>>{
+ favorite_id[PK][NN]
+ 
--
customaer_id
item_code
del_flag

}




entity "商品マスタ" as m_items <m_items><<M,MASTER_MARK_COLOR>>{
+ item_code[PK]
--
item_name
price
category_id
image
detail
del_flag
reg_date

}
entity "履歴テーブル" as d_history <d_history><<T,TEBUE_MARK_COLOR>>{
+ history_id[PK][NN]
--
customer_id
item_name
image
price
num
purchase_date
del_flg
}





d_purchase }o--o| m_customers 
 d_purchase_detail }|--|| d_purchase
 m_items }o--|| m_category
 m_favorite }o-- m_customers
 m_favorite }o-- m_items
 d_history ||--|| d_purchase
 d_history ||--|| d_purchase_detail
 d_history }|--o{ m_customers
 d_history }o--o{ m_favorite
 d_history }o--|{ m_items



@enduml
```





