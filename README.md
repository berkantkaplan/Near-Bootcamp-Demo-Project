# Festivals with Near

-This is a smart contract under which any community can request donations for organizing events, and others can donate.

## Build and Deploy the contract

```ts

After cloning ----> yarn


-----------------
yarn build:release
-------------------------
near dev-deploy ./build/release/simple.wasm
-----------------------------------
export CONTRACT=dev<123-456>
-------------------------
export OWNER=your-account.testnet
-----------------

```

# Class

## Festival
| Name | Type |
| ------ | ------ |
| owner | AccountId |
| id | u32 |
| festName | String |
| genre | String |
| country | String |
| date | String |
| donation | u128 |
| requestDonation | u128 |
| remainderDonation | u128 |
| maxDonationLimit | u128 |

# Functions

```ts

-addFest(festName:string,genre:string,country:string,date:string,requestDonation:u128) // Call function

-findFestById(id:u32)                                                                  // View function

-findFestByName(festName:string)                                                       // View function

-findFests(offset: u32, limit: u32=15)                                                 // View function

-donateFest(id: u32, donation:u8)                                                      // Call function         
```
# Explanation Functions

## addFest
```ts
- Takes ***festName*** , ***genre*** , ***country*** , ***date*** and ***requestDonation*** as parameters.
- ***date*** is the date of the festival.
- ***requestDonation*** is the donation amount requested for the festival.
```
## findFestById
```ts
- Takes ***id*** as parameter.
- The ids are unique, so you can find the festival whose id you know.
```
## findFestByName
```ts
- Takes ***festName*** as parameter.
- Shows the name of the festival whose id you know.
```
## findFests
```ts
- Takes ***offset*** and ***limit*** as parameters.
- the limit is capped at 15.
```
## donateFest
```ts
- Takes ***id*** and ***donation*** as parameters.
- The maximum donation amount is 50 NEAR.
- It does not make more donations than the remaining requested donation amount.
- It does not donate more than the remaining requested donation amount.
```
# Function Usage
|What Does It Do?|Example Call|
|---|---|
Add a Festival |`near call $CONTRACT addFest '{"festName":"'"Food Festival"'","genre":"'"Nutrition"'","country":"'"Africa"'","date":"'"17062022"'","requestDonation":"'"10000000000000000000000000000"'"}' --accountId $OWNER`|
Find Festival By Id |`near view $CONTRACT findFestById '{"id":'"234243234"'}' --accountId $OWNER`|
Find Festival By Name |`near view $CONTRACT findFestByName '{"festName":"'"Food Festival"'"}'`|
Get All Festivals|`near view $CONTRACT findFests '{"offset": 0}'`|
Donate Fesival|`near call $CONTRACT donateFest '{"id":'"234243234"', "donation" : '"$100000000000000000000000000"'}'  --accountId $OWNER --amount 100000000000000000000000000`|
