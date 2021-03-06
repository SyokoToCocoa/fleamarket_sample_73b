## usersテーブル

|Column|Type|Options|
|------|----|-------|
|nickname|string|null: false|
|email|string|null: false, unique: true|
|password|string|null: false|

### Association
- has_one :profile, dependent: :destroy
- has_one :sending_destination, dependent: :destroy
- has_one :credit_card, dependent: :destroy
- has_many :seller_items, foreign_key: "seller_id", class_name: "items"
- has_many :buyer_items, foreign_key: "buyer_id", class_name: "items"


## profileテーブル

|Column|Type|Options|
|------|----|-------|
|first_name|string|null: false|
|family_name|string|null: false|
|first_name_kana|string|null: false|
|family_name_kana|string|null: false|
|birth_year|date|null: false|
|birth_month|date|null: false|
|birth_day|date|null: false|
|user_id|references|null: false, foreign_key: true|

### Association
- belongs_to :user


## sending_destinationテーブル

|Column|Type|Options|
|------|----|-------|
|dest_first_name|string|null: false|
|dest_family_name|string|null: false|
|dest_first_name_kana|string|null: false|
|dest_family_name_kana|string|null: false|
|building_name|string|
|post_code|integer|null: false|
|prefecture_code|integer|null: false|
|house_number|string|null: false|
|phone_number|integer|unique: true|
|user_id|references|null: false, foreign_key: true|

### Association
- belongs_to :user


## credit_cardsテーブル

|Column|Type|Options|
|------|----|-------|
|card_number|integer|null: false, unique: true|
|expiration_year|integer|null: false|
|expiration_month|integer|null: false|
|security_code|integer|null: false|
|user_id|references|null: false, foreign_key: true|

### Association
- belongs_to :user


## itemsテーブル

|Column|Type|Options|
|------|----|-------|
|name|string|null: false|
|introduction|text|null: false|
|price|integer|null: false|
|item_img|integer|null: false, foreign_key: true|
|category|references|null: false, foreign_key: true|
|brand|references|foreign_key: true|
|item_condition|references|null: false, foreign_key: true|
|postage_payer|references|null: false, foreign_key: true|
|preparation_day|references|null: false, foreign_key: true|
|postage_type|references|null: false, foreign_key: true|
|prefecture_code|integer|null: false|
|trading_status|enum|null: false|
|seller|references|null: false, foreign_key: true|
|buyer|references|foreign_key: true|

### Association
- has_many :item_imgs, dependent: :destroy
- belongs_to :category
- belongs_to :brand
- belongs_to_active_hash :item_condition
- belongs_to_active_hash :postage_payer
- belongs_to_active_hash :preparation_days
- belongs_to_active_hash :postage_types
- belongs_to :seller, class_name: "user"
- belongs_to :buyer, class_name: "user"


## item_imgsテーブル

|Column|Type|Options|
|------|----|-------|
|item_id|references|null: false, foreign_key: true|
|url|string|null: false|

### Association
- belongs_to :item


## categoriesテーブル

|Column|Type|Options|
|------|----|-------|
|category|string|null: false|
|ancestry|string|null: false|

### Association
- has_many :items


## brandsテーブル

|Column|Type|Options|
|------|----|-------|
|brand|string|null: false|

### Association
- has_many :items


## item_conditionsテーブル

|Column|Type|Options|
|------|----|-------|
|item_condition|string|null: false|

### Association
- has_many :items


## postage_payersテーブル

|Column|Type|Options|
|------|----|-------|
|postage_payer|string|null: false|

### Association
- has_many :items


## preparation_daysテーブル

|Column|Type|Options|
|------|----|-------|
|preparation_day|string|null: false|

### Association
- has_many :items


## postage_typesテーブル

|Column|Type|Options|
|------|----|-------|
|postage_type|string|null: false|

### Association
- has_many :items
