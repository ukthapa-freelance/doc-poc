---
title: "Authentication Services"
description: ""
lead: ""
date: 2020-11-16T13:59:39+01:00
lastmod: 2020-11-16T13:59:39+01:00
draft: false
images: []
menu:
  docs:
    parent: "CRM"
weight: 201
toc: false
---

{{% method-block bgcolor="success" type="bg-blue" callmethod="GET" %}}
  /crm/v1/auth/email
{{% /method-block %}}

This service allows you to verify the customer's email ID. It requires input parameters like, email, correlationId, source, srdate, operation and destination. On successful verification the system will validate the email ID while signing up already exists in the system or not. If not the appropriate error code will be returned.

<section>

#### *Request Parameters*
| NAME        | TYPE          | DESCRIPTION  |
| ------------- |:-------------:| ----- |
| **email** (mandatory)    | ``string`` (header) | Provide the customer's email ID as the value. For example - adarsha_cds1@yopmail.com |
| **correlationId** (mandatory)    | ``string`` (header)      |   Provide the correlationId as the value. For example - 123e4567-e89b-12d3-a456-426614174000 |
| **Source** (mandatory) | ``string`` (header)      |    Provide the source as the value. For example - Selfcare |
| **srdate** (mandatory) | ``string`` (header)      |    Provide the date as the value. For example - 11-09-2021 |
| **Operation** (mandatory) | ``string`` (header)      |    Provide the operation as the value. For example - emailExists |
| **destination** (mandatory) | ``string`` (header)      |    Provide the destination as the value. |

{{< tabs "uniqueid" >}}
{{< tab "Request Header" >}}
{{< highlight java "linenos=table" >}}
correlationId:123e4567-e89b-12d3-a456-426614174000
email:adarsha_cds1@yopmail.com
operation:emailExists
destination:CRM
source:Selfcare
srDate:11-09-2021
{{< / highlight >}}
{{< /tab >}}
{{< tab "Response" >}}
{{< highlight java "linenos=table" >}}
{
  "response": {
    "success": "true",
    "result": {
      "response": "Email already exists."
    }
  }
}
{{< / highlight >}}
{{< /tab >}}
{{< tab "Client Error" >}}
{{< highlight java "linenos=table" >}}
{
  "response": {
    "result": {
      "arguments": {
        "statusCode": "400",
        "errorCode": "400 BAD_REQUEST",
        "errorMessage": "Header 'source' not present in the request."
      }
    },
    "success": "false"
  }
}
{{< / highlight >}}
{{< /tab >}}
{{< tab "Server Error" >}}
{{< highlight java "linenos=table" >}}
{
  "response": {
    "success": "false",
    "result": {
      "arguments": {
        "statusCode": "500",
        "errorCode": "Downstream error",
        "errorMessage": "- Not Able to connect with CRM."
      }
    }
  }
}
{{< / highlight >}}
{{< /tab >}}
{{< /tabs >}}
</section>

{{% method-block bgcolor="primary" type="bg-green" callmethod="POST" %}}
  /crm/v1/auth/otp
{{% /method-block %}}

This service is a validation service used when the customer wants to create a new password or has forgotten the password. It verifies the OTP to received for password generation.

This service requires correlationId, source, srdate, operation and destination along with the email ID, OTP and encrypted data in the API body. If the valid OTP is provided by the customer it will verify and allow to proceed with password creation successfully. If the OTP provided is wrong the appropriate error code will be returned.

<section>

### *Request Parameters*
| NAME        | TYPE           | DESCRIPTION  |
| ------------- |:-------------:| ----- |
| **correlationId** (mandatory)    | ``string`` (header)      |   Provide the correlationId as the value. For example - 123e4567-e89b-12d3-a456-426614174000 |
| **Source** (mandatory) | ``string`` (header)      |    Provide the source as the value. For example - Selfcare |
| **srdate** (mandatory) | ``string`` (header)      |    Provide the date as the value. For example - 11-09-2021 |
| **Operation** (mandatory) | ``string`` (header)      |    Provide the operation as the value. For example - sendOtp |
| **destination** (mandatory) | ``string`` (header)      |    Provide the destination as the value. |

### *Request Body Parameters*
| NAME        | TYPE           | DESCRIPTION  |
| ------------- |:-------------:| ----- |
| **email** (mandatory)    | ``string`` (body)      |   Provide the email Id as the value. For example -adarsha_cds3@yopmail.com |
| **encryptedOtp** (mandatory) | ``string`` (body)      |    Provide the encryptedOtp as the value. |
| **otp** (mandatory) | ``string`` (body)      |    Provide the OTP as the value. For example - 115695 |

{{< tabs "uniqueid1" >}}
{{< tab "Request Header" >}}
{{< highlight java "linenos=table" >}}
correlationId:123e4567-e89b-12d3-a456-426614174000
srDate:11-09-2021
source:Selfcare
destination:CRM
operation:sendOtp
{{< / highlight >}}
{{< /tab >}}
{{< tab "Request Body" >}}
{{< highlight java "linenos=table" >}}
{
    "email":"adarsha_cds3@yopmail.com",
    "encryptedOtp":"e1aa84d4a0a00d21f960b8938a23cb890e35609b080174b74753839587cbce42",
    "otp" : "115695"
}
{{< / highlight >}}
{{< /tab >}}
{{< tab "Response" >}}
{{< highlight java "linenos=table" >}}
{
  "response": {
    "success": "true",
    "result": {
      "message": "successfully verified OTP"
    }
  }
}
{{< / highlight >}}
{{< /tab >}}
{{< tab "Client Error" >}}
{{< highlight java "linenos=table" >}}
{
  "response": {
    "result": {
      "arguments": {
        "statusCode": "400",
        "errorCode": "400 BAD_REQUEST",
        "errorMessage": "Header 'source' not present in the request."
      }
    },
    "success": "false"
  }
}
{{< / highlight >}}
{{< /tab >}}
{{< /tabs >}}
</section>

{{% method-block bgcolor="success" type="bg-blue" callmethod="GET" %}}
  /crm/v1/auth/captcha
{{% /method-block %}}

This service is used to retrieve the captcha of the customer from the system for the purpose of authentication. It requires correlationId, source, srdate, operation and destination as input parameters. If the captcha clicked by the customer matches the captcha saved in the system the it will be successfully verified. If not appropriate error code will be returned.

<section>

#### *Request Parameters*
| NAME        | TYPE          | DESCRIPTION  |
| ------------- |:-------------:| ----- |
| **correlationId** (mandatory)    | ``string`` (header)      |   Provide the correlationId as the value. For example - 123e4567-e89b-12d3-a456-426614174000 |
| **Source** (mandatory) | ``string`` (header)      |    Provide the source as the value. For example - Selfcare |
| **srdate** (mandatory) | ``string`` (header)      |    Provide the date as the value. For example - 11-09-2021 |
| **Operation** (mandatory) | ``string`` (header)      |    Provide the operation as the value. For example - getCaptcha |
| **destination** (mandatory) | ``string`` (header)      |    Provide the destination as the value. |

{{< tabs "uniqueid2" >}}
{{< tab "Request Header" >}}
{{< highlight java "linenos=table" >}}
correlationId:123e4567-e89b-12d3-a456-426614174000
operation:getCaptcha
destination:CRM
source:Selfcare
srDate:11-09-2021
{{< / highlight >}}
{{< /tab >}}
{{< tab "Response" >}}
{{< highlight java "linenos=table" >}}
{
  "response": {
    "success": "true",
    "result": {
      "capthaImage": "http://localhost:31074/resources/captchaImages/fbcb0bbf8c79751facf4785d178607f8b5f7619b.jpg",
      "captchaHash": "c9891a983ba95d5a94bbeb6d05cd7fa39791384de05f2a1e464953b5265dcc49",
      "capthaAdImage": ""
    }
  }
}
{{< / highlight >}}
{{< /tab >}}
{{< tab "Client Error" >}}
{{< highlight java "linenos=table" >}}
{
  "response": {
    "result": {
      "arguments": {
        "statusCode": "400",
        "errorCode": "400 BAD_REQUEST",
        "errorMessage": "Header 'source' not present in the request."
      }
    },
    "success": "false"
  }
}
{{< / highlight >}}
{{< /tab >}}
{{< tab "Server Error" >}}
{{< highlight java "linenos=table" >}}
{
  "response": {
    "success": "false",
    "result": {
      "arguments": {
        "statusCode": "500",
        "errorCode": "Downstream error",
        "errorMessage": "- Not Able to connect with CRM."
      }
    }
  }
}
{{< / highlight >}}
{{< /tab >}}
{{< /tabs >}}
</section>

{{% method-block bgcolor="primary" type="bg-green" callmethod="POST" %}}
  /crm/v1/auth/captcha
{{% /method-block %}}

This service enables the user to provide a captcha for verification.

It requires correlationId, source, srdate, operation and destination as input parameters. If successful the captcha provided will be saved for a customer. If failed the appropriate error code will be returned.

<section>

### *Request Parameters*
| NAME        | TYPE           | DESCRIPTION  |
| ------------- |:-------------:| ----- |
| **correlationId** (mandatory)    | ``string`` (header)      |   Provide the correlationId as the value. For example - 123e4567-e89b-12d3-a456-426614174000 |
| **Source** (mandatory) | ``string`` (header)      |    Provide the source as the value. For example - Selfcare |
| **srdate** (mandatory) | ``string`` (header)      |    Provide the date as the value. For example - 11-09-2021 |
| **Operation** (mandatory) | ``string`` (header)      |    Provide the operation as the value. For example - verifyCaptcha |
| **destination** (mandatory) | ``string`` (header)      |    Provide the destination as the value. |

### *Request Body Parameters*
| NAME        | TYPE           | DESCRIPTION  |
| ------------- |:-------------:| ----- |
| **userCaptchaText** (mandatory)    | ``string`` (body)      |   Provide the captcha value. For example - PXJZ |
| **captchaHash** (mandatory) | ``string`` (body)      |    Provide the captchaHash value. For example - 56e1279915ab948fb149336779bbf6fbf692aec1d7d11d5aa988b29e05ce7fea |

{{< tabs "uniqueid3" >}}
{{< tab "Request Header" >}}
{{< highlight java "linenos=table" >}}
correlationId:123e4567-e89b-12d3-a456-426614174000
srDate:11-09-2021
source:Selfcare
destination:CRM
operation:verifyCaptcha
{{< / highlight >}}
{{< /tab >}}
{{< tab "Request Body" >}}
{{< highlight java "linenos=table" >}}
{
  "userCaptchaText": "PXJZ",
  "captchaHash": "56e1279915ab948fb149336779bbf6fbf692aec1d7d11d5aa988b29e05ce7fea"
}
{{< / highlight >}}
{{< /tab >}}
{{< tab "Response" >}}
{{< highlight java "linenos=table" >}}
{
  "response": {
    "success": "true",
    "result": {
      "message": "Captcha matched"
    }
  }
}
{{< / highlight >}}
{{< /tab >}}
{{< tab "Client Error" >}}
{{< highlight java "linenos=table" >}}
{
  "response": {
    "result": {
      "arguments": {
        "statusCode": "400",
        "errorCode": "400 BAD_REQUEST",
        "errorMessage": "Header 'source' not present in the request."
      }
    },
    "success": "false"
  }
}
{{< / highlight >}}
{{< /tab >}}
{{< /tabs >}}

{{% method-block bgcolor="primary" type="bg-green" callmethod="POST" %}}
  /crm/v1/otp
{{% /method-block %}}

This service enables the user to generate an OTP for resetting the password.

It requires correlationId, source, srdate, operation and destination as input parameters. If successful the OTP will be generated in the system for resetting the password. If failed the appropriate error code will be returned.

<section>

### *Request Parameters*
| NAME        | TYPE           | DESCRIPTION  |
| ------------- |:-------------:| ----- |
| **correlationId** (mandatory)    | ``string`` (header)      |   Provide the correlationId as the value. For example - 123e4567-e89b-12d3-a456-426614174000 |
| **Source** (mandatory) | ``string`` (header)      |    Provide the source as the value. For example - Selfcare |
| **srdate** (mandatory) | ``string`` (header)      |    Provide the date as the value. For example - 11-09-2021 |
| **Operation** (mandatory) | ``string`` (header)      |    Provide the operation as the value. For example - verifyOTP |
| **destination** (mandatory) | ``string`` (header)      |    Provide the destination as the value. |
| **type** (mandatory) | ``string`` (header)      |    Provide the type of OTP. |

### *Request Body Parameters*
| NAME        | TYPE           | DESCRIPTION  |
| ------------- |:-------------:| ----- |
| **userId** (mandatory)    | ``string`` (body)      |   Provide the userId as the value to send the OTP. For example - adarsha_cds3@yopmail.com |

{{< tabs "uniqueid4" >}}
{{< tab "Request Header" >}}
{{< highlight java "linenos=table" >}}
correlationId:123e4567-e89b-12d3-a456-426614174000
srDate:11-09-2021
source:Selfcare
destination:CRM
operation:verifyOTP
type:numbers
{{< / highlight >}}
{{< /tab >}}
{{< tab "Request Body" >}}
{{< highlight java "linenos=table" >}}
{
	"userId" : "adarsha_cds3@yopmail.com"
}
{{< / highlight >}}
{{< /tab >}}
{{< tab "Response" >}}
{{< highlight java "linenos=table" >}}
{
  "response": {
    "success": "true",
    "result": {
      "encryptedOtp": "57a70a39036974caa7e6392b9919846ab533829928b0c9ef06f1d4fbe7ea871f"
    }
  }
}
{{< / highlight >}}
{{< /tab >}}
{{< tab "Client Error" >}}
{{< highlight java "linenos=table" >}}
{
  "response": {
    "result": {
      "arguments": {
        "statusCode": "400",
        "errorCode": "400 BAD_REQUEST",
        "errorMessage": "Header 'source' not present in the request."
      }
    },
    "success": "false"
  }
}
{{< / highlight >}}
{{< /tab >}}
{{< tab "Server Error" >}}
{{< highlight java "linenos=table" >}}
{
  "response": {
    "success": "false",
    "result": {
      "arguments": {
        "statusCode": "500",
        "errorCode": "Downstream error",
        "errorMessage": "- Not Able to connect with CRM."
      }
    }
  }
}
{{< / highlight >}}
{{< /tab >}}
{{< /tabs >}}

</section>
