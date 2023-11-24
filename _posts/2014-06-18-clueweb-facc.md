---
layout: page
title: Notes on Dealing with the Freebase Annotations of the ClueWeb Corpora (FACC1)
---

#Notes on Dealing with the Freebase Annotations of the ClueWeb Corpora (FACC1)

The FACC1 data is released by Google and distributed by the Lemur project at <http://lemurproject.org/clueweb09/FACC1/> and <http://lemurproject.org/clueweb12/FACC1/>.

The following are some notes about dealing with this data.

## Format
The original format in which the data was released does not seem to be available. Instead, the Lemur project hosting the annotations provides them in an alternate form then easier to use. There, the information about each annotation is completely contained within a single line, and each line contains the encoding used to process the page.

It is important to note that offsets are given in terms of _bytes_ and not characters, so this needs to be taken into consideration.

## ClueWeb
ClueWeb, in both the 2009 and the 2012 versions, is released in the WARC file format. In this format, each document has a WARC header (not to be confused with the HTTP header) and contents (including the HTTP header).

```
WARC/0.18
WARC-Type: response
WARC-Target-URI: http://0xcc.net/binhacks/eabout.html
WARC-Warcinfo-ID: 9c8f4528-4bdf-4a57-970e-a637448313c5
WARC-Date: 2009-03-65T08:43:07-0800
WARC-Record-ID: <urn:uuid:b58a94c3-4c28-486f-aa1c-043d99aafcf0>
WARC-TREC-ID: clueweb09-en0000-99-00115
Content-Type: application/http;msgtype=response
WARC-Identified-Payload-Type:
Content-Length: 8963

HTTP/1.1 200 OK
Content-Type: text/html; charset=utf-8
Accept-Ranges: bytes
Date: Tue, 13 Jan 2009 22:46:01 GMT
Server: Apache/1.3.34 (Debian)
Connection: close
Last-Modified: Tue, 08 Jul 2008 10:43:50 GMT
ETag: "f8908-2201-487344e6"
Content-Length: 8705

ACTUAL CONTENT

```
 
 It is important to note that for text content, the charset information cannot be trusted. This is why the FACC1 annotations give an assumed charset with each annotation.
 

## Relevant code
* Reading Warc files for processing in Pig: <https://github.com/paepcke/PigIR>.
* Tools for processing annotations: <https://github.com/lemurproject/nopol>.