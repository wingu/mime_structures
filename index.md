---
layout: default
title: "Multipart MIME Email Structures"
---

#Multipart MIME Email Structures

A conformant  email client is minimally required to support the "mixed" and "digest" subtypes.  Other commonly used subtypes are "alternative", "message", "related", "report", "signed", "encrypted".  Note that many of these subparts can be nested.

The example patterns below are emails composed on the listed email clients filtered with of the courier [reformime](http://www.courier-mta.org/reformime.html) utility.  This anonymizes the messages and makes the structure more human-readable.

    $ cat test.eml | reformime -i | egrep 'content-|section'

<table class="table">
  <tr>
    <th>Pattern</th>
    <th>Outlook 2010</th>
    <th>OSX Mail v4.6</th>
    <th>Android Gmail v4.2.1</th>
  </tr>
  <tr>
    <td>plain text</td>
    <td>
      <pre>
section: 1
content-type: multipart/mixed
content-transfer-encoding: 8bit
charset: UTF-8
content-language: en-us
      </pre>
    </td>
    <td>
      <pre>
section: 1
content-type: text/plain
content-transfer-encoding: 7bit
      </pre>
</td>
    <td></td>
  </tr>
  <tr>
    <td>rich text</td>
    <td>
      <pre>
section: 1
content-type: multipart/alternative
content-transfer-encoding: 8bit
content-language: en-us
section: 1.1
content-type: text/plain
content-transfer-encoding: 7bit
section: 1.2
content-type: text/html
content-transfer-encoding: quoted-printable
	</pre>
      </td>
    <td>
      <pre>
section: 1
content-type: multipart/alternative
content-transfer-encoding: 8bit
section: 1.1
content-type: text/plain
content-transfer-encoding: 7bit
section: 1.2
content-type: text/html
content-transfer-encoding: 7bit
      </pre>
    </td>
    <td>
      <pre>
section: 1
content-type: multipart/alternative
content-transfer-encoding: 8bit
section: 1.1
content-type: text/plain
content-transfer-encoding: 8bit
section: 1.2
content-type: text/html
content-transfer-encoding: 8bit

      </pre>
</td>
  </tr>
  <tr>
    <td>attachment</td>
    <td>
      <pre>
section: 1
content-type: multipart/related
content-transfer-encoding: 8bit
content-language: en-us
section: 1.1
content-type: multipart/alternative
content-transfer-encoding: 8bit
section: 1.1.1
content-type: text/plain
content-transfer-encoding: 7bit
section: 1.1.2
content-type: text/html
content-transfer-encoding: quoted-printable
section: 1.2
content-type: image/jpeg
content-name: image001.jpg
content-transfer-encoding: base64
content-id: &lt;image001.jpg@01CDF571.231AA230&gt;
      </pre>
    </td>
    <td>
      <pre>
section: 1
content-type: multipart/mixed
content-transfer-encoding: 8bit
section: 1.1
content-type: text/plain
content-transfer-encoding: 7bit
section: 1.2
content-type: image/jpg
content-name: tiny_image.jpg
content-transfer-encoding: base64
content-disposition: inline
content-disposition-filename: tiny_image.jpg
	</pre>
    </td>
    <td>
      <pre>
section: 1
content-type: multipart/mixed
content-transfer-encoding: 8bit
section: 1.1
content-type: multipart/alternative
content-transfer-encoding: 8bit
section: 1.1.1
content-type: text/plain
content-transfer-encoding: 8bit
section: 1.1.2
content-type: text/html
content-transfer-encoding: 8bit
section: 1.2
content-type: image/jpeg
content-name: IMG_20130106_203051.jpg
content-transfer-encoding: base64
content-disposition: attachment
content-disposition-filename: IMG_20130106_203051.jpg
      </pre>
    </td>
  </tr>
  <tr>
    <td>multiple forwarded messages</td>
    <td>
      <pre>
section: 1
content-type: multipart/mixed
content-transfer-encoding: 8bit
content-language: en-us
section: 1.1
content-type: multipart/alternative
content-transfer-encoding: 8bit
section: 1.1.1
content-type: text/plain
content-transfer-encoding: 7bit
section: 1.1.2
content-type: text/html
content-transfer-encoding: quoted-printable
section: 1.2
content-type: message/rfc822
content-transfer-encoding: 7bit
content-disposition: attachment
section: 1.2.1
content-type: text/plain
content-transfer-encoding: 7bit
content-language: en-us
section: 1.3
content-type: message/rfc822
content-transfer-encoding: 7bit
content-disposition: attachment
section: 1.3.1
content-type: text/plain
content-transfer-encoding: 7bit
content-language: en-us
      </pre>
    </td>
    <td>
      <pre>
section: 1
content-type: multipart/mixed
content-transfer-encoding: 8bit
section: 1.1
content-type: message/rfc822
content-name: Welcome to OtherInbox!
content-transfer-encoding: 7bit
content-disposition: attachment
content-disposition-filename: Welcome to OtherInbox!
section: 1.1.1
content-type: multipart/mixed
content-transfer-encoding: 8bit
section: 1.1.1.1
content-type: multipart/alternative
content-transfer-encoding: 8bit
section: 1.1.1.1.1
content-type: text/plain
content-transfer-encoding: 7bit
section: 1.1.1.1.2
content-type: text/html
content-transfer-encoding: 7bit
section: 1.1.1.2
content-type: text/html
content-transfer-encoding: 7bit
section: 1.2
content-type: message/rfc822
content-name: Don't lose your free trial, Paul!
content-transfer-encoding: 7bit
content-disposition: attachment
content-disposition-filename: Don't lose your free trial, Paul!
section: 1.2.1
content-type: multipart/mixed
content-transfer-encoding: 8bit
section: 1.2.1.1
content-type: multipart/alternative
content-transfer-encoding: 8bit
section: 1.2.1.1.1
content-type: text/plain
content-transfer-encoding: 7bit
section: 1.2.1.1.2
content-type: text/html
content-transfer-encoding: 7bit
section: 1.2.1.2
content-type: multipart/alternative
content-transfer-encoding: 8bit
section: 1.2.1.2.1
content-type: text/plain
content-transfer-encoding: 7bit
content-id: &lt;4fe888e9a7b3_318df1213836448@domU-12-31-39-05-28-B1.mail&gt;
section: 1.2.1.2.2
content-type: text/html
content-transfer-encoding: 7bit
content-id: &lt;4fe888e9b5a1_318df121383652f@domU-12-31-39-05-28-B1.mail&gt;
	</pre>
    </td>
    <td></td>
  </tr>
</table>
