@startuml
entity "Client" as c {
* ID_client
--
**last_name**
**first_name**
middle_name
**birth_date**
**phone_number**
**password**
**passport**
}
entity "Card" as cd {
* ID_card
--
**card_number**
**expiry_date**
**cvc**
client_signature
**account_number**
* **card_type** : <<FK>> Card_Type.ID_type
* **client_id** : <<FK>> Client.ID_client
}
entity "Card_Type" as ct {
* ID_type
--
**tariff**
**payment_system**
**currency**
service_fee
}
entity "Account" as a {
* ID_account
--
**account_number**
**creation_date**
* **client_id** : <<FK>> Client.ID_client
}
entity "Mobile_App" as mp {
* ID_app
--
**authetification** : <<FK>> Client.ID_client
**client_info**
**services**
**offer_agreement**
}
entity "Orders" as o {
* ID_order
--
**creation_service_date**
* **client_id** : <<FK>> Client.ID_client
**agreement_id**
* **id_branch** : <<FK>> Branches.ID_branch
}
entity "Branches" as b {
* ID_branch
--
**number**
**address**
}
c ||--|{ a
c ||--|{ mp
mp ||--|{ o
cd }o--|{ ct
o ||--|| cd
o ||--o{ b
c ||--|{ cd
cd }o--|{ b
@enduml