<!--
Documentation research and outputs by LexTego Ltd.
Licensed under the Creative Commons Attribution-ShareAlike 4.0 International License.
See: https://creativecommons.org/licenses/by-sa/4.0/
-->
# Transaction Monitoring Service (TMS) API Documentation

This document describes the API endpoints for the Transaction Monitoring Service (TMS). The TMS API is designed to receive and process ISO 20022 financial messages for transaction monitoring purposes.

## Base URL

The base URL for all API endpoints is determined by the service's deployment environment. Typically, it will be something like:

```
http://<service-hostname>:<port>
```

The default port is `3000`, configurable via the `PORT` environment variable.

## Endpoints

The TMS API exposes the following endpoints:

### 1. Health Check

**Endpoint:** `GET /health` or `GET /`

**Description:**  This endpoint is used to check the health and availability of the TMS service.

**Request:**

- None

**Response (200 OK):**

```json
{
  "status": "UP"
}
```

### 2. Evaluate ISO 20022 Pain.001.001.11 Message

**Endpoint:** `POST /v1/evaluate/iso20022/pain.001.001.11`

**Description:** This endpoint accepts ISO 20022 `pain.001.001.11` (Customer Credit Transfer Initiation) messages for evaluation and processing.

**Request Body:**

- Content-Type: `application/json`
- Schema: [src/schemas/pain.001.json](./src/schemas/pain.001.json)

  ```json
  {
    "CstmrCdtTrfInitn": {
      // ... (refer to pain.001.json schema for detailed structure)
    }
  }
  ```

  **Example Request Body:**

  ```json
  {
    "CstmrCdtTrfInitn": {
      "GrpHdr": {
        "MsgId": "24988b914e3d4cf98a7659b2c45ce063258",
        "CreDtTm": "2021-12-03T12:40:14.000Z",
        "NbOfTxs": 1,
        "InitgPty": {
          "Nm": "April Blake Grant",
          "Id": {
            "PrvtId": {
              "DtAndPlcOfBirth": {
                "BirthDt": "1968-02-01",
                "CityOfBirth": "Unknown",
                "CtryOfBirth": "ZZ"
              },
              "Othr": [
                {
                  "Id": "+27730975224",
                  "SchmeNm": {
                    "Prtry": "MSISDN"
                  }
                }
              ]
            }
          },
          "CtctDtls": {
            "MobNb": "+27-730975224"
          }
        }
      },
      "PmtInf": {
        "PmtInfId": "5ab4fc7355de4ef8a75b78b00a681ed2569",
        "PmtMtd": "TRA",
        "ReqdAdvcTp": {
          "DbtAdvc": {
            "Cd": "ADWD",
            "Prtry": "Advice with transaction details"
          }
        },
        "ReqdExctnDt": {
          "Dt": "2021-12-03",
          "DtTm": "2021-12-03T12:40:14.000Z"
        },
        "Dbtr": {
          "Nm": "April Blake Grant",
          "Id": {
            "PrvtId": {
              "DtAndPlcOfBirth": {
                "BirthDt": "1968-02-01",
                "CityOfBirth": "Unknown",
                "CtryOfBirth": "ZZ"
              },
              "Othr": [
                {
                  "Id": "+27730975224",
                  "SchmeNm": {
                    "Prtry": "MSISDN"
                  }
                }
              ]
            }
          },
          "CtctDtls": {
            "MobNb": "+27-730975224"
          }
        },
        "DbtrAcct": {
          "Id": {
            "Othr": [
              {
                "Id": "+27730975224",
                "SchmeNm": {
                  "Prtry": "MSISDN"
                }
              }
            }
          ]
        },
        "Nm": "April Grant"
      },
      "DbtrAgt": {
        "FinInstnId": {
          "ClrSysMmbId": {
            "MmbId": "dfsp001"
          }
        }
      },
      "CdtTrfTxInf": {
        "PmtId": {
          "EndToEndId": "2c516801007642dfb892944dde1cf845"
        },
        "PmtTpInf": {
          "CtgyPurp": {
            "Prtry": "TRANSFER BLANK"
          }
        },
        "Amt": {
          "InstdAmt": {
            "Amt": {
              "Amt": 31020.89,
              "Ccy": "USD"
            }
          },
          "EqvtAmt": {
            "Amt": {
              "Amt": 31020.89,
              "Ccy": "USD"
            },
            "CcyOfTrf": "USD",
            "XchgRate": 1.00
          }
        },
        "ChrgBr": "DEBT",
        "CdtrAgt": {
          "FinInstnId": {
            "ClrSysMmbId": {
              "MmbId": "dfsp002"
            }
          }
        },
        "Cdtr": {
          "Nm": "Felicia Easton Quill",
          "Id": {
            "PrvtId": {
              "DtAndPlcOfBirth": {
                "BirthDt": "1935-05-08",
                "CityOfBirth": "Unknown",
                "CtryOfBirth": "ZZ"
              },
              "Othr": [
                {
                  "Id": "+27707650428",
                  "SchmeNm": {
                    "Prtry": "MSISDN"
                  }
                }
              ]
            }
          },
          "CtctDtls": {
            "MobNb": "+27-707650428"
          }
        },
        "CdtrAcct": {
          "Id": {
            "Othr": [
              {
                "Id": "+27707650428",
                "SchmeNm": {
                  "Prtry": "MSISDN"
                }
              }
            }
          ]
        },
        "Nm": "Felicia Quill"
      },
      "Purp": {
        "Cd": "MP2P"
      },
      "RgltryRptg": {
        "Dtls": {
          "Tp": "BALANCE OF PAYMENTS",
          "Cd": "100"
        }
      },
      "RmtInf": {
        "Ustrd": "Payment of USD 30713.75 from April to Felicia"
      },
      "SplmtryData": {
        "Envlp": {
          "Doc": {
            "Dbtr": {
              "FrstNm": "April",
              "MddlNm": "Blake",
              "LastNm": "Grant",
              "MrchntClssfctnCd": "BLANK"
            },
            "Cdtr": {
              "FrstNm": "Felicia",
              "MddlNm": "Easton",
              "LastNm": "Quill",
              "MrchntClssfctnCd": "BLANK"
            },
            "DbtrFinSvcsPrvdrFees": {
              "Ccy": "USD",
              "Amt": 307.14
            },
            "Xprtn": "2021-11-30T10:38:56.000Z"
          }
        }
      }
    },
    "SplmtryData": {
      "Envlp": {
        "Doc": {
          "InitgPty": {
            "InitrTp": "CONSUMER",
            "Glctn": {
              "Lat": "-3.1609",
              "Long": "38.3588"
            }
          }
        }
      }
    }
  }
  ```

**Response (200 OK):**

```json
{
  "message": "Transaction is valid",
  "data": {
    // ... (the original pain.001.001.11 request body)
  }
}
```

**Response (500 Internal Server Error):**

```
Failed to process execution request.
{
    // ... (Error details in JSON format)
}
```

**Conditional Availability:**

This endpoint is conditionally available based on the `QUOTING` environment variable. If `QUOTING` is set to `true`, this endpoint is enabled. If `QUOTING` is `false` or not set, this endpoint might be disabled in the routing configuration.

**Authentication:**

If authentication is enabled (see section on Authentication), this endpoint requires a valid Bearer token in the `Authorization` header with the claim `POST_V1_EVALUATE_ISO20022_PAIN_001_001_11`.

### 3. Evaluate ISO 20022 Pain.013.001.09 Message

**Endpoint:** `POST /v1/evaluate/iso20022/pain.013.001.09`

**Description:** This endpoint accepts ISO 20022 `pain.013.001.09` (Creditor Payment Activation Request) messages for evaluation and processing.

**Request Body:**

- Content-Type: `application/json`
- Schema: [src/schemas/pain.013.json](./src/schemas/pain.013.json)

  ```json
  {
    "CdtrPmtActvtnReq": {
      // ... (refer to pain.013.json schema for detailed structure)
    }
  }
  ```

  **Example Request Body:**

  ```json
  {
    "CdtrPmtActvtnReq": {
      "GrpHdr": {
        "MsgId": "42665509efd844da90caf468e891aa52256",
        "CreDtTm": "2021-12-03T12:40:16.000Z",
        "NbOfTxs": 1,
        "InitgPty": {
          "Nm": "April Blake Grant",
          "Id": {
            "PrvtId": {
              "DtAndPlcOfBirth": {
                "BirthDt": "1968-02-01",
                "CityOfBirth": "Unknown",
                "CtryOfBirth": "ZZ"
              },
              "Othr": [
                {
                  "Id": "+27730975224",
                  "SchmeNm": {
                    "Prtry": "MSISDN"
                  }
                }
              ]
            }
          },
          "CtctDtls": {
            "MobNb": "+27-730975224"
          }
        }
      },
      "PmtInf": {
        "PmtInfId": "5ab4fc7355de4ef8a75b78b00a681ed2254",
        "PmtMtd": "TRA",
        "ReqdAdvcTp": {
          "DbtAdvc": {
            "Cd": "ADWD",
            "Prtry": "Advice with transaction details"
          }
        },
        "ReqdExctnDt": {
          "DtTm": "2021-12-03T12:40:14.000Z"
        },
        "XpryDt": {
          "DtTm": "2021-11-30T10:38:56.000Z"
        },
        "Dbtr": {
          "Nm": "April Blake Grant",
          "Id": {
            "PrvtId": {
              "DtAndPlcOfBirth": {
                "BirthDt": "1968-02-01",
                "CityOfBirth": "Unknown",
                "CtryOfBirth": "ZZ"
              },
              "Othr": [
                {
                  "Id": "+27730975224",
                  "SchmeNm": {
                    "Prtry": "MSISDN"
                  }
                }
              ]
            }
          },
          "CtctDtls": {
            "MobNb": "+27-730975224"
          }
        },
        "DbtrAcct": {
          "Id": {
            "Othr": [
              {
                "Id": "+27730975224",
                "SchmeNm": {
                  "Prtry": "MSISDN"
                }
              }
            }
          ]
        },
        "Nm": "April Grant"
      },
      "DbtrAgt": {
        "FinInstnId": {
          "ClrSysMmbId": {
            "MmbId": "dfsp001"
          }
        }
      },
      "CdtTrfTxInf": {
        "PmtId": {
          "EndToEndId": "2c516801007642dfb892944dde1cf845"
        },
        "PmtTpInf": {
          "CtgyPurp": {
            "Prtry": "TRANSFER BLANK"
          }
        },
        "Amt": {
          "InstdAmt": {
            "Amt": {
              "Amt": 31020.89,
              "Ccy": "USD"
            }
          },
          "EqvtAmt": {
            "Amt": {
              "Amt": 31020.89,
              "Ccy": "USD"
            },
            "CcyOfTrf": "USD"
          }
        },
        "ChrgBr": "DEBT",
        "CdtrAgt": {
          "FinInstnId": {
            "ClrSysMmbId": {
              "MmbId": "dfsp002"
            }
          }
        },
        "Cdtr": {
          "Nm": "Felicia Easton Quill",
          "Id": {
            "PrvtId": {
              "DtAndPlcOfBirth": {
                "BirthDt": "1935-05-08",
                "CityOfBirth": "Unknown",
                "CtryOfBirth": "ZZ"
              },
              "Othr": [
                {
                  "Id": "+27707650428",
                  "SchmeNm": {
                    "Prtry": "MSISDN"
                  }
                }
              ]
            }
          },
          "CtctDtls": {
            "MobNb": "+27-707650428"
          }
        },
        "CdtrAcct": {
          "Id": {
            "Othr": [
              {
                "Id": "+27707650428",
                "SchmeNm": {
                  "Prtry": "MSISDN"
                }
              }
            }
          ]
        },
        "Nm": "Felicia Quill"
      },
      "Purp": {
        "Cd": "MP2P"
      },
      "RgltryRptg": {
        "Dtls": {
          "Tp": "BALANCE OF PAYMENTS",
          "Cd": "100"
        }
      },
      "SplmtryData": {
        "Envlp": {
          "Doc": {
            "PyeeRcvAmt": {
              "Amt": {
                "Amt": 30713.75,
                "Ccy": "USD"
              }
            },
            "PyeeFinSvcsPrvdrFee": {
              "Amt": {
                "Amt": 153.57,
                "Ccy": "USD"
              }
            },
            "PyeeFinSvcsPrvdrComssn": {
              "Amt": {
                "Amt": 30.71,
                "Ccy": "USD"
              }
            }
          }
        }
      }
    },
    "SplmtryData": {
      "Envlp": {
        "Doc": {
          "InitgPty": {
            "Glctn": {
              "Lat": "-3.1609",
              "Long": "38.3588"
            }
          }
        }
      }
    }
  }
  }
  ```

**Response (200 OK):**

```json
{
  "message": "Transaction is valid",
  "data": {
    // ... (the original pain.013.001.09 request body),
    "TxTp": "pain.013.001.09"
  }
}
```

**Response (500 Internal Server Error):**

```
Failed to process execution request.
{
    // ... (Error message string)
}
```

**Conditional Availability:**

This endpoint is conditionally available based on the `QUOTING` environment variable. If `QUOTING` is set to `true`, this endpoint is enabled. If `QUOTING` is `false` or not set, this endpoint might be disabled in the routing configuration.

**Authentication:**

If authentication is enabled (see section on Authentication), this endpoint requires a valid Bearer token in the `Authorization` header with the claim `POST_V1_EVALUATE_ISO20022_PAIN_013_001_09`.

### 4. Evaluate ISO 20022 Pacs.008.001.10 Message

**Endpoint:** `POST /v1/evaluate/iso20022/pacs.008.001.10`

**Description:** This endpoint accepts ISO 20022 `pacs.008.001.10` (Financial Institution To Financial Institution Customer Credit Transfer) messages for evaluation and processing.

**Request Body:**

- Content-Type: `application/json`
- Schema: [src/schemas/pacs.008.json](./src/schemas/pacs.008.json)

  ```json
  {
    "FIToFICstmrCdtTrf": {
      // ... (refer to pacs.008.json schema for detailed structure)
    }
  }
  ```

  **Example Request Body:**

  ```json
  {
    "FIToFICstmrCdtTrf": {
      "GrpHdr": {
        "MsgId": "24e80c9836f6437e8aa46cbb3fbdd5b1",
        "CreDtTm": "2024-05-27T13:57:33.890Z",
        "NbOfTxs": 1,
        "SttlmInf": {
          "SttlmMtd": "CLRG"
        }
      },
      "CdtTrfTxInf": {
        "PmtId": {
          "InstrId": "5ab4fc7355de4ef8a75b78b00a681ed2",
          "EndToEndId": "fe252acd9f1742d0ad9d74000ecc57d8"
        },
        "IntrBkSttlmAmt": {
          "Amt": {
            "Amt": 531.81,
            "Ccy": "XTS"
          }
        },
        "InstdAmt": {
          "Amt": {
            "Amt": 531.81,
            "Ccy": "XTS"
          }
        },
        "XchgRate": "1.00",
        "ChrgBr": "DEBT",
        "ChrgsInf": {
          "Amt": {
            "Amt": 0,
            "Ccy": "XTS"
          },
          "Agt": {
            "FinInstnId": {
              "ClrSysMmbId": {
                "MmbId": "dfsp001"
              }
            }
          }
        },
        "InitgPty": {
          "Nm": "April Blake Grant",
          "Id": {
            "PrvtId": {
              "DtAndPlcOfBirth": {
                "BirthDt": "1968-02-01",
                "CityOfBirth": "Unknown",
                "CtryOfBirth": "ZZ"
              },
              "Othr": [
                {
                  "Id": "+27730975224",
                  "SchmeNm": {
                    "Prtry": "MSISDN"
                  }
                }
              ]
            }
          },
          "CtctDtls": {
            "MobNb": "+27-730975224"
          }
        },
        "Dbtr": {
          "Nm": "April Blake Grant",
          "Id": {
            "PrvtId": {
              "DtAndPlcOfBirth": {
                "BirthDt": "1999-05-09",
                "CityOfBirth": "Unknown",
                "CtryOfBirth": "ZZ"
              },
              "Othr": [
                {
                  "Id": "60409827ba274853a2ec2475c64566d5",
                  "SchmeNm": {
                    "Prtry": "TAZAMA_EID"
                  }
                }
              ]
            }
          },
          "CtctDtls": {
            "MobNb": "+27-730975224"
          }
        },
        "DbtrAcct": {
          "Id": {
            "Othr": [
              {
                "Id": "7473251533b34fe891fa8b0d1691d375",
                "SchmeNm": {
                  "Prtry": "MSISDN"
                }
              }
            }
          ]
        },
        "Nm": "April Grant"
      },
      "DbtrAgt": {
        "FinInstnId": {
          "ClrSysMmbId": {
            "MmbId": "dfsp001"
          }
        }
      },
      "CdtrAgt": {
        "FinInstnId": {
          "ClrSysMmbId": {
            "MmbId": "dfsp002"
          }
        }
      },
      "Cdtr": {
        "Nm": "Felicia Easton Quill",
        "Id": {
          "PrvtId": {
            "DtAndPlcOfBirth": {
              "BirthDt": "1935-05-08",
              "CityOfBirth": "Unknown",
              "CtryOfBirth": "ZZ"
            },
            "Othr": [
              {
                "Id": "1d495a2f710e436089677dcc789f279d",
                "SchmeNm": {
                  "Prtry": "TAZAMA_EID"
                }
              }
            ]
          }
        },
        "CtctDtls": {
          "MobNb": "+27-707650428"
        }
      },
      "CdtrAcct": {
        "Id": {
          "Othr": [
            {
              "Id": "f58d206a6ada4a34a372dfbd66b17c6f",
              "SchmeNm": {
                "Prtry": "MSISDN"
              }
            }
          ]
        },
        "Nm": "Felicia Quill"
      },
      "Purp": {
        "Cd": "MP2P"
      }
    },
    "RgltryRptg": {
      "Dtls": {
        "Tp": "BALANCE OF PAYMENTS",
        "Cd": "100"
      }
    },
    "RmtInf": {
      "Ustrd": "Generic payment description"
    },
    "SplmtryData": {
      "Envlp": {
        "Doc": {
          "Xprtn": "2021-11-30T10:38:56.000Z",
          "InitgPty": {
            "Glctn": {
              "Lat": "-3.1609",
              "Long": "38.3588"
            }
          }
        }
      }
    }
  }
  }
  ```

**Response (200 OK):**

```json
{
  "message": "Transaction is valid",
  "data": {
    // ... (the original pacs.008.001.10 request body)
  }
}
```

**Response (500 Internal Server Error):**

```
Failed to process execution request.
{
    // ... (Error details in JSON format)
}
```
**Authentication:**

If authentication is enabled (see section on Authentication), this endpoint requires a valid Bearer token in the `Authorization` header with the claim `POST_V1_EVALUATE_ISO20022_PACS_008_001_10`.

### 5. Evaluate ISO 20022 Pacs.002.001.12 Message

**Endpoint:** `POST /v1/evaluate/iso20022/pacs.002.001.12`

**Description:** This endpoint accepts ISO 20022 `pacs.002.001.12` (Financial Institution To Financial Institution Payment Status) messages for evaluation and processing.

**Request Body:**

- Content-Type: `application/json`
- Schema: [src/schemas/pacs.002.json](./src/schemas/pacs.002.json)

  ```json
  {
    "FIToFIPmtSts": {
      // ... (refer to pacs.002.json schema for detailed structure)
    }
  }
  ```

  **Example Request Body:**

  ```json
  {
    "FIToFIPmtSts": {
      "GrpHdr": {
        "MsgId": "e24562287a264651b0c42a3de9ea44fe",
        "CreDtTm": "2024-05-27T14:02:33.890Z"
      },
      "TxInfAndSts": {
        "OrgnlInstrId": "5ab4fc7355de4ef8a75b78b00a681ed2",
        "OrgnlEndToEndId": "fe252acd9f1742d0ad9d74000ecc57d8",
        "TxSts": "ACCC",
        "ChrgsInf": [
          {
            "Amt": {
              "Amt": 0,
              "Ccy": "USD"
            },
            "Agt": {
              "FinInstnId": {
                "ClrSysMmbId": {
                  "MmbId": "dfsp001"
                }
              }
            }
          },
          {
            "Amt": {
              "Amt": 0,
              "Ccy": "USD"
            },
            "Agt": {
              "FinInstnId": {
                "ClrSysMmbId": {
                  "MmbId": "dfsp001"
                }
              }
            }
          },
          {
            "Amt": {
              "Amt": 0,
              "Ccy": "USD"
            },
            "Agt": {
              "FinInstnId": {
                "ClrSysMmbId": {
                  "MmbId": "dfsp002"
                }
              }
            }
          }
        ],
        "AccptncDtTm": "2023-06-02T07:52:31.000Z",
        "InstgAgt": {
          "FinInstnId": {
            "ClrSysMmbId": {
              "MmbId": "dfsp001"
            }
          }
        },
        "InstdAgt": {
          "FinInstnId": {
            "ClrSysMmbId": {
              "MmbId": "dfsp002"
            }
          }
        }
      }
    }
  }
  ```

**Response (200 OK):**

```json
{
  "message": "Transaction is valid",
  "data": {
    // ... (the original pacs.002.001.12 request body)
  }
}
```

**Response (500 Internal Server Error):**

```
Failed to process execution request.
{
    // ... (Error details in JSON format)
}
```

**Authentication:**

If authentication is enabled (see section on Authentication), this endpoint requires a valid Bearer token in the `Authorization` header with the claim `POST_V1_EVALUATE_ISO20022_PACS_002_001_12`.

---

## Authentication

API authentication can be enabled or disabled via the `AUTHENTICATED` environment variable.

- **`AUTHENTICATED=true`**: Authentication is **enabled**.  All message processing endpoints (`pain.001`, `pain.013`, `pacs.008`, `pacs.002`) will require a valid Bearer token in the `Authorization` header of the request. The token must be validated against a public key (configured via `CERT_PATH_PUBLIC` environment variable). Each endpoint requires a specific claim to be present in the token for authorization.
- **`AUTHENTICATED=false` (default)**: Authentication is **disabled**. No token is required to access the message processing endpoints.

**Token Format:**

The API expects a JWT (JSON Web Token) as a Bearer token.

**Authorization Claims:**

Each message processing endpoint is protected by a specific claim:

| Endpoint                                     | Required Claim                                        |
|----------------------------------------------|-------------------------------------------------------|
| `POST /v1/evaluate/iso20022/pain.001.001.11` | `POST_V1_EVALUATE_ISO20022_PAIN_001_001_11`          |
| `POST /v1/evaluate/iso20022/pain.013.001.09` | `POST_V1_EVALUATE_ISO20022_PAIN_013_001_09`          |
| `POST /v1/evaluate/iso20022/pacs.008.
