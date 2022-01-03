
# date verbs
## date.convertToTimeZone
#### Syntax
date.convertToTimeZone (date, string)

#### Params
The date param is the date you want to convert to a different time zone. 

The string says how far from GMT and in what direction the other time zone is. For example -5 would be the string for the east coast of the United States, meaning five hours earlier than GMT. "0" is GMT. This param is optional, if not specified it is "0".

The string param does not have to represent a whole hour. For example Central Indian Time is "+5:30".

#### Returns
The date, expressed in the indicated time zone. 

If x is a date returned by this routine, you can use the JavaScript date functions to get components of a time, getHours, getMinutes, etc and they will return the correct values for the indicated time zone.

This is a core routine for building blogs that might be published by software running in a time zone different from the author of the blog. 

#### Examples
undefined

## date.dayGreaterThanOrEqual
#### Syntax
date.dayGreaterThanOrEqual (d1, d2)

#### Params
Both parameters are JavaScript date objects. 

#### Returns
true if the first date is on the same day as the second, or if the first date is later than the second. 

#### Notes
This verb is useful in determining which version of software you're running, if you have the publication date of a new version. Also useful to see if a timer has expired. 

#### Example
undefined

## date.netStandardString
#### Syntax
date.netStandardString (date)

#### Params
date is a JavaScript date object.

#### Returns
A <a href="https://tools.ietf.org/html/rfc822">RFC 822</a> version of the date. 

#### Notes
This is the format that's required for RSS feeds, OPML files and mail protocols. 

It's a human and machine readable way of expressing of dates. 

#### Examples
undefined

undefined

## date.sameDay
#### Syntax
date.sameDay (d1, d2)

#### Params
Both parameters are JavaScript date objects. 

#### Returns
true if the dates are on the same day, false otherwise.

#### Examples
undefined

undefined

## date.sameMonth
#### Syntax
date.sameMonth (d1, d2)

#### Params
Both parameters are JavaScript date objects. 

#### Returns
true if the dates are in the same month, false otherwise.

#### Examples
undefined

undefined

## date.secondsSince
#### Syntax
date.secondsSince (date)

#### Params
date is a JavaScript date object.

#### Returns
The number of seconds since the date. 

#### Notes
Useful when you want to know how long something took. 

#### Example
undefined

## date.tomorrow
#### Syntax
date.tomorrow (date)

#### Params
date is a JavaScript date object.

#### Returns
The result of adding 24 hours from the date.

#### Example
undefined

## date.yesterday
#### Syntax
date.yesterday (date)

#### Params
date is a JavaScript date object.

#### Returns
The result of subtracting 24 hours from the date.

#### Example
undefined

