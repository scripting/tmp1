
# dns verbs
## dns.getDomainName
#### Syntax
dns.getDomainName (dottedid)

#### Returns
The domain name associated with the dotted id. This is often referred to as "reverse DNS."

#### Common error
There is no domain associated with the provided dotted id.

#### Example
undefined

#### Limits
It only returns one domain name, but there might be more than one domain mapped to a given IP address. 

## dns.getDottedId
#### Syntax
dns.getDottedId (name)

#### Returns
Return the dotted id associated with the name. This is often referred to as "DNS lookup."

#### Common error
The domain is not defined. 

#### Bug
When there's an error, the error message is undefined.

#### Example
undefined

undefined

undefined

