# quoted-printable

## Index 
- [Intro](#Intro)
- [Dependencies](#Dependencies)
- [Test dependencies](#Test-dependencies)
- [Foreign dependencies](#Foreign-dependencies)
- [API](#API)
- [Examples](#Examples)
- [Author(s)](#Authors)
- [Maintainer(s)](#Maintainers)
- [Version](#Version) 
- [License](#License) 
- [Tags](#Tags) 

## Intro 
Implementation of [QP encoding](https://en.wikipedia.org/wiki/Quoted-printable) ported from Chibi Scheme.

## Dependencies 
None

## Test-dependencies 
None

## Foreign-dependencies 
None

## API 

### (cyclone quoted-printable)

#### [procedure] `(qp-encode bv start-col max-col separator)`

Allow for RFC1522 quoting for headers by always escaping `?` and `_`

#### [procedure] `(quoted-printable-encode-string src . o)`

Return a quoted-printable encoded representation of the input
according to the official standard as described in RFC2045.

`?` and `_` are always encoded for compatibility with RFC1522
encoding, and soft newlines are inserted as necessary to keep each
lines length less than `max-col` (default 76).  The starting
column may be overridden with `start-col` (default 0).

#### [procedure] `(quoted-printable-encode . o)`

Variation of the above to read and write to ports.

#### [procedure] `(quoted-printable-encode-bytevector . o)`

#### [procedure] `(quoted-printable-encode-header encoding . o)`

Return a quoted-printable encoded representation of string as
above, wrapped in `...` as per RFC1522, split across
multiple MIME-header lines as needed to keep each lines length
less than `max-col`.  The string is encoded as is, and the
encoding `enc` is just used for the prefix, i.e. you are
responsible for ensuring `str` is already encoded according to
`enc`.

#### [procedure] `(quoted-printable-decode-string src . o)`

Return a quoted-printable decoded representation of `str`.  If
`mime-header?` is specified and true, _ will be decoded as as
space in accordance with RFC1522.  No errors will be raised on
invalid input.

#### [procedure] `(quoted-printable-decode-bytevector  . o)`

#### [procedure] `(quoted-printable-decode . o)`

Variation of the above to read and write to ports.


## Examples
```scheme
(import (scheme base) (cyclone quoted-printable) (cyclone test))
(test-group "quoted-printable"

  (test "J'interdis aux marchands de vanter trop leur marchandises. Car ils se font vite pédagogues et t'enseignent comme but ce qui n'est par essence qu'un moyen, et te trompant ainsi sur la route à suivre les voilà bientôt qui te dégradent, car si leur musique est vulgaire ils te fabriquent pour te la vendre une âme vulgaire."
        (quoted-printable-decode-string
         "J'interdis aux marchands de vanter trop leur marchandises. Car ils se font =
vite p=C3=A9dagogues et t'enseignent comme but ce qui n'est par essence qu'=
un moyen, et te trompant ainsi sur la route =C3=A0 suivre les voil=C3=A0 bi=
ent=C3=B4t qui te d=C3=A9gradent, car si leur musique est vulgaire ils te f=
abriquent pour te la vendre une =C3=A2me vulgaire.")))
(test-exit)
```

## Author(s)
Alex Shinn

## Maintainer(s) 
Justin Ethier

## Version 
0.2

## License 
BSD

## Tags 
networking


