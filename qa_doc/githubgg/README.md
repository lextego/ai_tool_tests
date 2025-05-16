<!--
Documentation research and outputs by LexTego Ltd.
Licensed under the Creative Commons Attribution-ShareAlike 4.0 International License.
See: https://creativecommons.org/licenses/by-sa/4.0/
-->
# Transaction Monitoring Service (TMS) - Quick Guide

This is a quick guide to the Transaction Monitoring Service (TMS) API. For detailed information, please refer to the [full documentation](https://github.com/tazama-lf/docs/blob/dev/Product/transaction-monitoring-service-api.md).

**What is TMS?**

The Transaction Monitoring Service (TMS) API helps you validate and process financial transactions, specifically ISO20022 messages. It currently supports:

* **pain.001.001.11** (Customer Credit Transfer Initiation)
* **pain.013.001.09** (Creditor Payment Activation Request)
* **pacs.008.001.10** (FIToFICustomer Credit Transfer)
* **pacs.002.001.12** (FIToFIPayment Status Report)

**API Endpoints**

The base URL for the API is assumed to be `http://<your-tms-service-address>`.

| Endpoint                                    | Message Type          | Description                                                                 |
| ------------------------------------------- | --------------------- | --------------------------------------------------------------------------- |
| `/v1/evaluate/iso20022/pain.001.001.11`     | `pain.001.001.11`     | Submit a pain.001 message for validation and processing.                  |
| `/v1/evaluate/iso20022/pain.013.001.09`     | `pain.013.001.09`     | Submit a pain.013 message for validation and processing.                  |
| `/v1/evaluate/iso20022/pacs.008.001.10`     | `pacs.008.001.10`     | Submit a pacs.008 message for validation and processing.                  |
| `/v1/evaluate/iso20022/pacs.002.001.12`     | `pacs.002.001.12`     | Submit a pacs.002 message for validation and processing.                  |
| `/health`                                   | Health Check          | Check if the service is running. Returns `{"status": "UP"}` if healthy. |

**Request Method:** `POST` for all transaction endpoints.

**Request Body:**  JSON payload conforming to the ISO20022 message schema. See examples below.

**Response:**

* **200 OK:** Transaction is considered valid. Response body includes:
    ```json
    {
      "message": "Transaction is valid",
      "data": { /* ... original transaction object ... */ }
    }
    ```
* **400 Bad Request:** Request format is invalid.
* **401 Unauthorized:** Authentication is required and failed (if enabled).
* **500 Internal Server Error:**  Error during processing. Response body will contain an error message.

**Example Requests (using `curl`)**

**1. pain.001.001.11**

```bash
curl -X POST \
  -H "Content-Type: application/json" \
  -d '{
  "CstmrCdtTrfInitn": {
    "GrpHdr": {
      "MsgId": "test-pain001-msg-id",
      "CreDtTm": "2024-05-28T10:00:00.000Z",
      "NbOfTxs": 1,
      "InitgPty": {
        "Nm": "Sender Name"
      }
    },
    "PmtInf": {
      "PmtInfId": "test-payment-info-id",
      "PmtMtd": "TRA",
      "ReqdExctnDt": {
        "Dt": "2024-05-28"
      },
      "Dbtr": {
        "Nm": "Debtor Name"
      },
      "DbtrAcct": {
        "Id": {
          "Othr": [
            {
              "Id": "debtor-account-id",
              "SchmeNm": {
                "Prtry": "ACCOUNT"
              }
            }
          ]
        }
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
          "EndToEndId": "test-e2e-id"
        },
        "Amt": {
          "InstdAmt": {
            "Amt": {
              "Amt": 100.00,
              "Ccy": "USD"
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
          "Nm": "Creditor Name"
        },
        "CdtrAcct": {
          "Id": {
            "Othr": [
              {
                "Id": "creditor-account-id",
                "SchmeNm": {
                  "Prtry": "ACCOUNT"
                }
              }
            ]
          }
        }
      }
    }
  }
}' \
  http://<your-tms-service-address>/v1/evaluate/iso20022/pain.001.001.11
```

**(Replace `<your-tms-service-address>` with the actual address of your TMS service.)**

**2. pain.013.001.09**

```bash
curl -X POST \
  -H "Content-Type: application/json" \
  -d '{
  "CdtrPmtActvtnReq": {
    "GrpHdr": {
      "MsgId": "test-pain013-msg-id",
      "CreDtTm": "2024-05-28T10:00:00.000Z",
      "NbOfTxs": 1,
      "InitgPty": {
        "Nm": "Sender Name"
      }
    },
    "PmtInf": {
      "PmtInfId": "test-payment-info-id",
      "PmtMtd": "TRA",
      "ReqdExctnDt": {
        "DtTm": "2024-05-28T10:00:00.000Z"
      },
      "Dbtr": {
        "Nm": "Debtor Name"
      },
      "DbtrAcct": {
        "Id": {
          "Othr": [
            {
              "Id": "debtor-account-id",
              "SchmeNm": {
                "Prtry": "ACCOUNT"
              }
            }
          ]
        }
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
          "EndToEndId": "test-e2e-id"
        },
        "Amt": {
          "InstdAmt": {
            "Amt": {
              "Amt": 100.00,
              "Ccy": "USD"
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
          "Nm": "Creditor Name"
        },
        "CdtrAcct": {
          "Id": {
            "Othr": [
              {
                "Id": "creditor-account-id",
                "SchmeNm": {
                  "Prtry": "ACCOUNT"
                }
              }
            ]
          }
        }
      }
    }
  }
}' \
  http://<your-tms-service-address>/v1/evaluate/iso20022/pain.013.001.09
```

**3. pacs.008.001.10**

```bash
curl -X POST \
  -H "Content-Type: application/json" \
  -d '{
  "FIToFICstmrCdtTrf": {
    "GrpHdr": {
      "MsgId": "test-pacs008-msg-id",
      "CreDtTm": "2024-05-28T10:00:00.000Z",
      "NbOfTxs": 1,
      "SttlmInf": {
        "SttlmMtd": "CLRG"
      }
    },
    "CdtTrfTxInf": {
      "PmtId": {
        "InstrId": "test-instruction-id",
        "EndToEndId": "test-e2e-id"
      },
      "IntrBkSttlmAmt": {
        "Amt": {
          "Amt": 100.00,
          "Ccy": "USD"
        }
      },
      "InstdAmt": {
        "Amt": {
          "Amt": 100.00,
          "Ccy": "USD"
        }
      },
      "ChrgBr": "DEBT",
      "ChrgsInf": {
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
      "InitgPty": {
        "Nm": "Sender Name",
        "Id": {
          "PrvtId": {
            "DtAndPlcOfBirth": {
              "BirthDt": "1970-01-01",
              "CityOfBirth": "Unknown",
              "CtryOfBirth": "ZZ"
            },
            "Othr": [
              {
                "Id": "sender-id",
                "SchmeNm": {
                  "Prtry": "PARTY_ID"
                }
              }
            ]
          }
        },
        "CtctDtls": {
          "MobNb": "+1-555-123-4567"
        }
      },
      "Dbtr": {
        "Nm": "Debtor Name",
        "Id": {
          "PrvtId": {
            "DtAndPlcOfBirth": {
              "BirthDt": "1970-01-01",
              "CityOfBirth": "Unknown",
              "CtryOfBirth": "ZZ"
            },
            "Othr": [
              {
                "Id": "debtor-id",
                "SchmeNm": {
                  "Prtry": "PARTY_ID"
                }
              }
            ]
          }
        },
        "CtctDtls": {
          "MobNb": "+1-555-123-4567"
        }
      },
      "DbtrAcct": {
        "Id": {
          "Othr": [
            {
              "Id": "debtor-account-id",
              "SchmeNm": {
                "Prtry": "ACCOUNT"
              }
            }
          ]
        },
        "Nm": "Debtor Account"
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
        "Nm": "Creditor Name",
        "Id": {
          "PrvtId": {
            "DtAndPlcOfBirth": {
              "BirthDt": "1970-01-01",
              "CityOfBirth": "Unknown",
              "CtryOfBirth": "ZZ"
            },
            "Othr": [
              {
                "Id": "creditor-id",
                "SchmeNm": {
                  "Prtry": "PARTY_ID"
                }
              }
            ]
          }
        },
        "CtctDtls": {
          "MobNb": "+1-555-123-4567"
        }
      },
      "CdtrAcct": {
        "Id": {
          "Othr": [
            {
              "Id": "creditor-account-id",
              "SchmeNm": {
                "Prtry": "ACCOUNT"
              }
            }
          ]
        },
        "Nm": "Creditor Account"
      },
      "Purp": {
        "Cd": "MP2P"
      }
    }
  }
}' \
  http://<your-tms-service-address>/v1/evaluate/iso20022/pacs.008.001.10
```

**4. pacs.002.001.12**

```bash
curl -X POST \
  -H "Content-Type: application/json" \
  -d '{
  "FIToFIPmtSts": {
    "GrpHdr": {
      "MsgId": "test-pacs002-msg-id",
      "CreDtTm": "2024-05-28T10:00:00.000Z"
    },
    "TxInfAndSts": {
      "OrgnlInstrId": "test-instruction-id",
      "OrgnlEndToEndId": "test-e2e-id",
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
        }
      ],
      "AccptncDtTm": "2024-05-28T10:00:00.000Z",
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
}' \
  http://<your-tms-service-address>/v1/evaluate/iso20022/pacs.002.001.12
```

**Repository:** [GitHub - frmscoe/tms-service](https://github.com/frmscoe/tms-service)

For any questions or further assistance, please refer to the full documentation or contact the development team.
