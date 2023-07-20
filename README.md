# TLDExtract
<code>TLDExtract</code> is a pure Swift library to allows you to get the public suffix of a domain name using [the Public Suffix List](http://www.publicsuffix.org). You can find alternatives for other languages at [publicsuffix.org](https://publicsuffix.org/learn/).<br/>

## What are domains?

Domain names are the unique, human-readable Internet addresses of websites. They are made up of three parts: a top-level domain (a.k.a. TLD), a second-level domain name, and an optional subdomain.

<img src="Metadata/domain-diagram.svg" alt="drawing" width="480" style="width:100%; max-width: 480px;"/>

## Feature

- Extract root domain, top level domain, second level domain, subdomain from url and hostname
- Foundation URL and String support
- IDNA support
- Multi platform support

## Requirements

- iOS 9.3 or later
- macOS 10.12 or later
- tvOS 10.2 or later
- Swift 4.2 or later
- Python 2.7 or Python 3

## Installation

// TODO

## Usage

### Initialization

```swift
import TLDExtract

let extractor = TLDExtract()
```
### Extraction

#### Passing argument as String

Extract an url:

```swift
let urlString: String = "https://www.github.com/gumob/TLDExtract"
guard let result: TLDResult = extractor.parse(urlString) else { return }

print(result.rootDomain)        // Optional("github.com")
print(result.topLevelDomain)    // Optional("com")
print(result.secondLevelDomain) // Optional("github")
print(result.subDomain)         // Optional("www")
```

Extract a hostname:

```swift
let hostname: String = "gumob.com"
guard let result: TLDResult = extractor.parse(hostname) else { return }

print(result.rootDomain)        // Optional("gumob.com")
print(result.topLevelDomain)    // Optional("com")
print(result.secondLevelDomain) // Optional("gumob")
print(result.subDomain)         // nil
```

Extract an unicode hostname:

```swift
let hostname: String = "www.ラーメン.寿司.co.jp"
guard let result: TLDResult = extractor.parse(hostname) else { return }

print(result.rootDomain)        // Optional("寿司.co.jp")
print(result.topLevelDomain)    // Optional("co.jp")
print(result.secondLevelDomain) // Optional("寿司")
print(result.subDomain)         // Optional("www.ラーメン")
```

Extract a punycoded hostname (Same as above):

```swift
let hostname: String = "www.xn--4dkp5a8a.xn--sprr0q.co.jp")"
guard let result: TLDResult = extractor.parse(hostname) else { return }

print(result.rootDomain)        // Optional("xn--sprr0q.co.jp")
print(result.topLevelDomain)    // Optional("co.jp")
print(result.secondLevelDomain) // Optional("xn--sprr0q")
print(result.subDomain)         // Optional("www.xn--4dkp5a8a")
```

#### Passing argument as Foundation URL

Extract an unicode url: <br/>
URL class in Foundation Framework does not support unicode URLs by default. You can use URL extension as a workaround
```swift
let urlString: String = "http://www.ラーメン.寿司.co.jp"
let url: URL = URL(unicodeString: urlString)
guard let result: TLDResult = extractor.parse(url) else { return }

print(result.rootDomain)        // Optional("www.ラーメン.寿司.co.jp")
print(result.topLevelDomain)    // Optional("co.jp")
print(result.secondLevelDomain) // Optional("寿司")
print(result.subDomain)         // Optional("www.ラーメン")
```

Encode an url by passing argument as percent encoded string (Same as above):
```swift
let urlString: String = "http://www.ラーメン.寿司.co.jp".addingPercentEncoding(withAllowedCharacters: .urlQueryAllowed)!
let url: URL = URL(string: urlString)
print(urlString)                // http://www.%E3%83%A9%E3%83%BC%E3%83%A1%E3%83%B3.%E5%AF%BF%E5%8F%B8.co.jp

guard let result: TLDResult = extractor.parse(url) else { return }

print(result.rootDomain)        // Optional("www.ラーメン.寿司.co.jp")
print(result.topLevelDomain)    // Optional("co.jp")
print(result.secondLevelDomain) // Optional("寿司")
print(result.subDomain)         // Optional("www.ラーメン")
```

## Copyright

TLDExtract is released under MIT license, which means you can modify it, redistribute it or use it however you like.
