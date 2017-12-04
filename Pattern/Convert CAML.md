# Simple query converter


## Functions
> `$caml = ConvertTo-KFCAML -Query "<string>"`
> `$caml = Get-KFNormalizedCAML -Query "<string>"`

## Example
> `{{item-internal-fieldname}} == string "hello"`

## Combinations
> AND `{{item-internal-fieldname}} == string "hello" & {{item-internal-fieldname}} == string "hello"`
> OR `{{item-internal-fieldname}} == string "hello" | {{item-internal-fieldname}} == string "hello"`

## Operators
> `==`
> `!=`
> `<=`
> `>=`
> `<`
> `>`
> `|=`
> `=`| 
> `~`

## Datetyps
> `string`
> `int` | `integer`
> `date`
> `dateutc`
> `datetime`
> `datetimeutc`
> `userid`
> `lookupid`
> `lookuptext`
> `null`

## Wildcards
> `[[Today]]`
> `[[UserId]]`