# dig

например, посмотреть значение `TXT`-записи `_acme-challenge` для домена **example.com**:

{% include cl.htm cmd="dig txt _acme-challenge.example.com"
small='...
;; ANSWER SECTION:
_acme-challenge.swim.org.ua. 3600 IN	TXT	"ykaOuGpYzhEHIq2TF1-0GWUpUqF1roF7gd66TC7a_iM"
...' %}

## Help

{% include cl.htm cmd="dig -h" %}

## Links

<https://2whois.ru/?t=dig>
