# Database Design Guideline

## Basic concepts

* Goal of database design is that we need to make it clear the following things:
  * Purpose of tables & columns
  * What kind of data should be stored
* For example, use abbreviation forms makes people unclear about the meaning.
  * `fb` may be facebook, but can be `feedback`.

## Table naming

* Table name must be a
  * Plural form
  * Snake case
* Relation table must be
  * [singular form of parent table] _ [plural form of children table]. like `user_addresses`.
* Must not use any kind of abbreviation forms
  * must not use `user_addrs`, must be `user_addresses`

## Column naming and Types

### Basic rules

* Column name must be:
  * Snake case
* Must not use any kind of abbreviation forms
  * `device_sn` must be `device_serial_number`
  * must not use `fb_token`, use `facebook_token`

### Primary Key

* All table must have a column named `id` as a primary key. It must be unsigned bigint(20) and be auto incremented. Name and type are fixed and must not be changed.
* You must not use composite primary key. On some cases, such as relation tables, composite key might be a better way theoretically. But some wireframes assumed that all tables have single primary key, so we fixed to use `id` as a primary key to make the situation simpler.

### created_at, updated_at and deleted_at

* All tables must have `created_at` and `updated_at` for storing created datetime and updated datetime. Types for both are `timestamp`.
* The tables which uses soft delete must have `deleted_at`. It must also be `timestamp` type.
* Name and types are fixed and must not be changed.

### Datetime
* if you want to store datetime to the database, must use `_at` postfix and use int and store unixtimestamp.
* Never use datetime type because MySQL datetime type cannot store timezone and it may cause of bugs and confusion.
* Use timestamp only for `created_at`, `updated_at` and `deteled_at` because it is used in the framework.

### Gender
* Gender ( male, female...) must use varchar as datatype and store string like type ( `male` & `female`).
* Must not use integer value like 1 means male, 2 means female.
* It is because number is not human readable and also it may increase the kind of genders ( Now facebook has 50 genders).
* And Model must define constants of all options

### Status
* Many table can have a column which represents some kind of the "status" of the record.
  * Blog post can have a status of the post ( "published" / "draft")
  * Approval procedure can have a status of approval ( "submitted", "approved", "rejected")
* This kind of status must be stored as "text" such as "published" / "submitted".
* Must not use number ( 1 .. published. 0 .. draft). Because it is quite difficult to understand what it indicated in the future.
* And number is a bit difficult to extend sometimes. if there are 3 status and want to add 2 more status between statys 1 and 2. on that case, work flow becomes 1->4->5->2->3 and looks difficult to understand. So text might be more flexible from the human psychological point of vuiews.
* And Model must define constants of all options

### Types
* Sometimes table must store "type" of the entity.
  * uploaded file can have a type that "text", "image", "video"...
* Type also be a text from the same reason of Status.
* And Model must define constants of all options

### Code
* sometimes we need to store code. Such as country code, currency code, and so on. on that case, you should use `_code` prefix such as `country_code` or `currency_code`.

### Prefix & Postfix

Some data types must follow this rules of prefix/postfix. It is used fof

|column type|prefix|postfix|data type|
|:--|:--|:--|:--|
|boolean flags|`is_` or `has_`|-|tinyint|
|datetime|-|`_at`|unsigned int(10)|
|date|-|`_date`|date|
|reference to other table|-|`_id`|unsigned bigint(20)|
|status|-|_status|varchar|
|type|-|_type|varchar|
