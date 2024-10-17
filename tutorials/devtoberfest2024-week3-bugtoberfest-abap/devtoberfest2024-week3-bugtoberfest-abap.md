---
auto_validation: true
time: 20
author_name: Sheena M K
author_profile: https://github.com/sheenamk
tags: [ tutorial>beginner, topic>cloud ]
primary_tag: topic>cloud
parser: v2
---

# 🟡 Devtoberfest 2024 - Fun Friday Week 3 - Bugtoberfest ABAP
This is the ABAP Bug Hunt!

## You will learn
- How to have fun hunting for bugs in code.

## Prerequisites
- Basic to intermediate knowledge of ABAP.


## Intro
As a part of Devtoberfest 2024 Fun Friday events, we have a bug hunt written in multiple languages for you to complete! The questions will range from easy to spot to a little more difficult, requiring some knowledge of the individual languages to complete. Each question will have 1 to 10 bugs and no bug should require running the code for the bug to appear.

## Hints to count the bugs
If the same bugs are repeated in a single line then, it's counted as 1. 
Eg: Missing multiple braces () in the same statement is considered as 1

Every unique bug in the same line will be counted separately. 

Remember to have fun and enjoy the bug hunt. Happy hunting!

This tutorial is part of the Devtoberfest 2024, a celebration of and for Developers. For more information, see the [Devtoberfest Group](https://groups.community.sap.com/t5/devtoberfest/gh-p/Devtoberfest).

![Devtoberfest](promo-image-kasimir-square.png)

&nbsp;

For specifics on the Devtoberfest contest and the grand prize, see this [Devtoberfest 2024 Contest blog](https://community.sap.com/t5/devtoberfest-blog-posts/devtoberfest-2024-contest/ba-p/13781593)

&nbsp;

### Question 1 (Easy)

Find the bugs in the following code.

<pre lang="ABAP">
CLASS ztest
 DEFINITION
  PUBLIC
  FINAL
  CREATE PUBLIC .
  PUBLIC SECTION.
    METHODS test_value.
    METHODS test_value1.
  PROTECTED SECTION.
  PRIVATE SECTION.
ENDCLASS.

CLASS ztest
 IMPLEMENTATION.
  METHOD test_value2.
  ENDMETHOD.
  METHOD test_value1
  ENDCLASS.
</pre>

### Question 2 (Medium)

Find the bugs in the following code.

<pre lang="ABAP">
@AccessControl.authorizationCheck: #NOT_REQUIRED
@EndUserText.label: 'Carrier View - CDS Data Model'
@Search.searchable: true
define view entity ZTest
  as selectfrom /dmo/flight as Flight
  association [1] to /DMO/I_Carrier as _Airline 
{
      @UI.lineItem: [ { position: 10, label: 'Airline'} ]
      @Search.defaultSearchElement: true
      @Search.fuzzinessThreshold: 0.7
      @ObjectModel.text.association: '_Airline'
  key Flight.carrier_id     as AirlineID,
      @UI.lineItem: [ { position: 20, label: 'Connection Number' } ]
  key Flight.connection_id  as ConnectionID,
      @UI.lineItem: [ { position: 30, label: 'Flight Date' } ]
  key Flight.flight_date    as FlightDate,
      @UI.lineItem: [ { position: 40, label: 'Price' } ]
      @Semantics.amount.currencyCode: 'CurrencyCode'
      Flight.price          as Price,
      Flight.currency_code  as CurrencyCode,
      @Semantics.amount.currencyCode: 'CurrencyCode'
      case
       when price <= 1000 or price is initial
        then cast(price as /dmo/flight_price preserving type)
       else
         cast( 1000 + (cast(price as abap.numc(16,2)) - 1000 ) * 
division(9,10,2) as /dmo/flight_price)
       end as

  /* Associations */
      _Airline
}
</pre>

### Question 3 (Hard)

Find the bugs in the following code.

<pre lang="ABAP">
@AbapCatalog.viewEnhancementCategory: [#NONE]
@abapcatalog.sqlViewName: 'ZTESt1'
@AccessControl.authorizationCheck: '#NOT_REQUIRED'
@EndUserText.label: 'Test'
@Metadata.ignorePropagatedAnnotations: true
@ObjectModel.usageType:{
   serviceQuality: #X,
   sizeCategory: #S,
   dataClass: #MIXED
}
define view entity ZTest!
  with parameters
    P_Currency :/dmo/currency_code
  as select from /dmo/travel
  association [0] to /DMO/I_Overall_Status_VH_Text as _Status on $projection.Status = _Status.OverallStatus
{
  key travel_id                 as TravelId,
      description               as Description,
      total_price               as TotalPrice,
      currency_code             as CurrencyCode,
      concat_with_space(cast(total_price as abap.char( 20) ),
      $parameters.P_Curency,1) as AmountInCurrency,
      @Consumption.valueHelpDefinition: [{ element: { name:
      '/DMO/I_Overall_Status_VH',entity: 'OverallStatus' } }]
      status                    as Status,
      _Status.Text              as OverallStatus,
}

</pre>

