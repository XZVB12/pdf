# malice-pdf

[![Circle CI](https://circleci.com/gh/malice-plugins/pdf.png?style=shield)](https://circleci.com/gh/malice-plugins/pdf) [![License](http://img.shields.io/:license-mit-blue.svg)](http://doge.mit-license.org) [![Docker Stars](https://img.shields.io/docker/stars/malice/pdf.svg)](https://hub.docker.com/r/malice/pdf/) [![Docker Pulls](https://img.shields.io/docker/pulls/malice/pdf.svg)](https://hub.docker.com/r/malice/pdf/) [![Docker Image](https://img.shields.io/badge/docker%20image-55.9MB-blue.svg)](https://hub.docker.com/r/malice/pdf/)

Malice PDF Plugin

> This repository contains a **Dockerfile** of **malice/pdf**.

---

### Dependencies

- [malice/alpine](https://hub.docker.com/r/malice/alpine/)

### Installation

1.  Install [Docker](https://www.docker.io/).
2.  Download [trusted build](https://hub.docker.com/r/malice/pdf/) from public [DockerHub](https://hub.docker.com): `docker pull malice/pdf`

### Usage

```bash
$ docker run --rm -v /path/to/malware:/malware malice/pdf --help

Usage: pdfscan [OPTIONS] COMMAND [ARGS]...

  Malice PDF Plugin

  Author: blacktop <https://github.com/blacktop>

Options:
  --version   print the version
  -h, --help  Show this message and exit.

Commands:
  scan  scan a file
  web   start web service
```

#### Scanning

```bash
$ docker run --rm -v /path/to/malware:/malware malice/pdf scan --help

Usage: pdfscan scan [OPTIONS] FILE_PATH

  Malice PDF Plugin.

Options:
  -v, --verbose            verbose output
  -t, --table              output as Markdown table
  -x, --proxy PROXY        proxy settings for Malice webhook endpoint
                           [$MALICE_PROXY]
  -c, --callback ENDPOINT  POST results back to Malice webhook
                           [$MALICE_ENDPOINT]
  --elasticsearch HOST     elasticsearch address for Malice to store
                           results [$MALICE_ELASTICSEARCH]
  --timeout SECS           malice plugin timeout (default: 10)
                           [$MALICE_TIMEOUT]
  -h, --help               Show this message and exit.
```

This will output to stdout and POST to malice results API webhook endpoint.

## Sample Output

### JSON:

```json
{
  "pdf": {
    "streams": {},
    "peepdf": {},
    "pdfid": {
      "heuristics": {
        "embeddedfile": {
          "reason": "`/EmbeddedFile` flag(s) detected",
          "score": 0.9
        },
        "nameobfuscation": {
          "reason": "no hex encoded flags detected",
          "score": 0
        },
        "suspicious": {},
        "triage": {
          "reason": "sample is likely malicious and requires further analysis",
          "score": 1
        }
      },
      "countChatAfterLastEof": "0",
      "errorMessage": "",
      "dates": {
        "date": []
      },
      "nonStreamEntropy": "4.896895",
      "header": "%PDF-1.1",
      "version": "0.2.4",
      "entropy": "",
      "totalEntropy": "7.873045",
      "isPdf": "True",
      "keywords": {
        "keyword": [
          {
            "count": 9,
            "hexcodecount": 0,
            "name": "obj"
          },
          {
            "count": 9,
            "hexcodecount": 0,
            "name": "endobj"
          },
          {
            "count": 2,
            "hexcodecount": 0,
            "name": "stream"
          },
          {
            "count": 2,
            "hexcodecount": 0,
            "name": "endstream"
          },
          {
            "count": 1,
            "hexcodecount": 0,
            "name": "xref"
          },
          {
            "count": 1,
            "hexcodecount": 0,
            "name": "trailer"
          },
          {
            "count": 1,
            "hexcodecount": 0,
            "name": "startxref"
          },
          {
            "count": 1,
            "hexcodecount": 0,
            "name": "/Page"
          },
          ...SNIP...
          {
            "count": 0,
            "hexcodecount": 0,
            "name": "/Colors > 2^24"
          }
        ]
      },
      "countEof": "1",
      "streamEntropy": "7.970107",
      "errorOccured": "False"
    }
  }
}
```

### Markdown:

---

#### pdf

#### PDFiD

- **PDF Header:** `%PDF-1.1`
- **Total Entropy:** `7.873045`
- **Entropy In Streams:** `7.970107`
- **Entropy Out Streams:** `4.896895`
- **Count %% EOF:** `1`
- **Data After EOF:** `0`

**Embedded File:**

- **Score:** `0.9`
- **Reason:** `/EmbeddedFile` flag(s) detected

**Triage:**

- **Score:** `1.0`
- **Reason:** sample is likely malicious and requires further analysis

| Keyword        | Count |
| -------------- | ----- |
| obj            | 9     |
| endobj         | 9     |
| stream         | 2     |
| endstream      | 2     |
| xref           | 1     |
| trailer        | 1     |
| startxref      | 1     |
| /Page          | 1     |
| /Encrypt       | 0     |
| /ObjStm        | 0     |
| /JS            | 1     |
| /JavaScript    | 1     |
| /AA            | 0     |
| /OpenAction    | 1     |
| /AcroForm      | 0     |
| /JBIG2Decode   | 0     |
| /RichMedia     | 0     |
| /Launch        | 0     |
| /EmbeddedFile  | 1     |
| /XFA           | 0     |
| /Colors > 2^24 | 0     |

---

## Documentation

- [To write results to ElasticSearch](https://github.com/malice-plugins/pdf/blob/master/docs/elasticsearch.md)
- [To create a PDF scan micro-service](https://github.com/malice-plugins/pdf/blob/master/docs/web.md)
- [To post results to a webhook](https://github.com/malice-plugins/pdf/blob/master/docs/callback.md)

### Issues

Find a bug? Want more features? Find something missing in the documentation? Let me know! Please don't hesitate to [file an issue](https://github.com/malice-plugins/pdf/issues/new)

### CHANGELOG

See [`CHANGELOG.md`](https://github.com/malice-plugins/pdf/blob/master/CHANGELOG.md)

### Contributing

[See all contributors on GitHub](https://github.com/malice-plugins/pdf/graphs/contributors).

Please update the [CHANGELOG.md](https://github.com/malice-plugins/pdf/blob/master/CHANGELOG)

### Credits

Heavily (if not entirely) influenced by CSE-CST's [alsvc_pdfid](https://bitbucket.org/cse-assemblyline/alsvc_pdfid) and [alsvc_peepdf](https://bitbucket.org/cse-assemblyline/alsvc_peepdf)

### TODO

- [ ] add PDFiD
- [ ] add pdf-parser for streams
- [ ] add peepdf for JS

### License

MIT Copyright (c) 2016-2018 **blacktop**
