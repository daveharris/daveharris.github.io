---
layout: post
title: VLOOKUP Excel Function
tags:
- excel
---
Have you ever had list of status flags that have a meaning and within excel be able to change the number for the actual meaning?  Then this is for you!

Assume you have this data:

<table>
  <tr>
    <th>Customer Id </th>
    <th>Payment Type </th>
  </tr>
  <tr>
    <td>1</td>
    <td>2</td>
  </tr>
  <tr>
    <td>2</td>
    <td>0</td>
  </tr>
  <tr>
    <td>3</td>
    <td>1</td>
  </tr>
</table>

And you have a set of Payment Types:

<table>
  <tr>
    <th>Payment Type Code </th>
    <th>Payment Description </th>
  </tr>
  <tr>
    <td>0</td>
    <td>Cash</td>
  </tr>
  <tr>
    <td>1</td>
    <td>Eftpos</td>
  </tr>
  <tr>
    <td>2</td>
    <td>Credit Card</td>
  </tr>
</table>


If you have this data in an Excel spreadsheet you can use the `VLOOKUP` function to translate these numbers into meanings.  

The `VLOOKUP` function is defined as `VLOOKUP(lookup_value, table_array, col_index_num, range_lookup)` where:

* lookup_value: the id that is to be looked up
* table_array: the table which holds the key and the value (can be on another sheet)
* col_index_num: the column number within the table which holds the value
* range_lookup: boolean to specify if 'approximate' values should be looked up

Therefore a simple formula could be: `=VLOOKUP(B15, A26:B29, 2, FALSE)`

If you need to perform this action on a whole table of data and need to keep it in a constant column, and the lookup table is on another sheet, this can be used: `=VLOOKUP(B2,Sheet2!$A$2:$B$5, 2, FALSE)`

I cannot claim the credit for this albeit simple and well-documented function, all credit goes to [Phil Wheeler](http://wheeler.kiwi.nz)
