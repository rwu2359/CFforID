## CFforID
Custom functions to convert to FMTID and FMFID

## Required
This is only of any value in OData 4.01 which arrived in the middle of the FMS 21 cycle, but I do recommend using the latest version of FileMaker Server

## Description
These custom functions are helpers to convert table and field names into FMTID and FMFID so that they can be used to abstract OData queries.
They are being launched at EngageU 2025 in Anterp at the start on November

Where it is required the header block indicates a dependancy on the listPositionCF, which is used return the value in listB based on the positino of an item in listA. Helpful as we have TableIDs and TableNames which give a list of numbers and alist of string, but they are in sync.

## Purpose
These function help with creating code which will survive renaming - which is a breaking issue for most of our current queries.

The table ID has been exposed for quite a while and within each table the fiedd ID is a number increasing from 1.
In OData we can see in the metadata an FMFID, and this is a combination of the table ID and field ID.

The field ID is left shifted and added to the table ID, This is a 32-bit shift, so times the field ID by 2 ^ 32 (4294967296) then add the ID.
To convert back from FMFID to the Field Id, just do the reverse. Take off the table ID, divide by 2^32 and then look that value up in the field names, or even better go and read the excellent article by Andrew Duncan from databuzz -- [querying the system tables(https://www.databuzz.com.au/accessing-base-tables-in-claris-filemaker-2023/)]

## Brucie bonus
There is one extra step that is helpful here. If your query has a Prefer header with value fmodata.entity-ids then all the returned keys will be FMFID. If you use that data with these functions you can then do a set field by name, and your inbound data JSONGetElement() will also not break.

## FileMaker file
Simple with layout calculations to show the custom functions in operation

#### version history
    1. 25_10_10, initial release
