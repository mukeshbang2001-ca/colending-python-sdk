# colending-python-client
# Integration Document

The following are the endpoints to be called during and pre/post disbursement state of a loan.

## Authentication

Authentication details and host will be shared privately.

## Workflow

**Create Loan** is the initial endpoint to be called to create a loan. Loan will be processed in the background and the status of loan will be provided through the configured Webhook. However, the client can also poll the server via the **Get Loan Details** endpoint to know the loan's status(**Get Loan Details** is rate throttled and polling this API will be restricted). Loan's shall be considered rejected if proper response is not available within 10minutes.

All other endpoints are self-explanatory and can be retried upto 3 times before marking as failure.

## Allowed Links

All Link attributes should contain
1. Accessible File Link URL which can be Public/Expiry URL/Whitelisted File Server Link(Write to tech.colending@credavenue.com for obtaining our IP address to whitelist)
2. File Link URL with Header Authentication (Header values should be shared with tech.colending@credavenue.com)

## Allowed Fields Length
<table border=\"2\" cellspacing=\"0\" cellpadding=\"6\" rules=\"groups\" frame=\"hsides\">

<colgroup>

<col  class=\"org-left\" />

<col  class=\"org-left\" />

</colgroup>
<thead>
<tr>
<th scope=\"col\" class=\"org-left\">Data Type</th>
<th scope=\"col\" class=\"org-left\">Max Length</th>
</tr>
</thead>

<tbody>
<tr>
<td class=\"org-left\">String</td>
<td class=\"org-left\">65,535 bytes</td>
</tr>

<tr>
<td class=\"org-left\">Float</td>
<td class=\"org-left\">8 bytes</td>
</tr>

<tr>
<td class=\"org-left\">Integer</td>
<td class=\"org-left\">4 bytes</td>
</tr>

<tr>
<td class=\"org-left\">Date</td>
<td class=\"org-left\">10 characters</td>
</tr>

</tbody>
</table>

# Webhooks

Webhooks can be configured for the below events

1. Loan status change

    Response Payload : 
    {
        \"product_id\": \"\",
        \"client_loan_id\": \"\",
        \"principal_amount\": \"\",
        \"interest_rate\": \"\",
        \"tenure\": \"\",
        \"tenure_frequency\": \"MONTHLY\",
        \"cibil_score\": \"\",
        \"purpose\": \"\",
        \"repayment_frequency\":\"\",
        \"number_of_repayments\": \"\",
        \"status\": \"\",
        \"principal_outstanding\": \"\",
        \"reject_reason\": \"\"
    }
    
    Statuses : ['new', 'approved', 'rejected', 'agreement_signed', 'dropped', 'disbursement_ready', 'disbursed', 'matured', 'partner_settled']
   
2. Loan disbursement details (Disbursed through razorpay)

    Callback Payload: 
    {
        \"client_loan_id\":\"\",
        \"status\":\"borrower_disbursed\",
        \"disbursed_date\":\"\",
        \"utr_number\":\"\",
        \"disbursement_type\":\"\",
        \"payment_reversed\": \"TRUE/FALSE\",
        \"disbursement_amount\":\"\",
        \"investor_disbursed_amount\": \"\",
        \"partner_disbursed_amount\": \"\",
        \"differential_interest\":\"\",
        \"investor_differential_interest\":\"\",
        \"partner_differential_interest\":\"\",
        \"differential_days\":\"\",
        \"interest_start_date\":\"\",
        \"investor_processing_fee\":\"\",
        \"partner_processing_fee\":\"\",
        \"investor_stamp_duty\":\"\",
        \"partner_stamp_duty\":\"\",
        \"investor_documentation_charges\":\"\",
        \"partner_documentation_charges\":\"\"
    }

Provide the following details to configure the webhooks
1. callback URL
2. authentication for the callback URL (header authentication)



# Validations

**PAN**

- **Example**: ABGPA1232P
- **Sequence**: First five digits will be alpha, next four will be Numerical and again last single digit will be alpha

**GSTIN**

- **Example**: 33AAACT2727Q1ZV
- **Sequence**: First two digits is Numerical, Next is PAN sequence as specified above, again thirteenth digit will be numerical, fourteenth digit is alpha, last digit will be alpha or numerical

**CIN**

- **Example**: U65929TN2017PTC117196
- **Sequence**: First digit is Alpha, next 5 numeric digits, next two alpha, next set of 4 numeric digits, Next 3 alpha, last 6 numeric digits

**PASSPORT**

- **Example**: A2096457
- **Sequence**: Total 8 digits, first digit is Alpha, remaining digits are numerical

**AADHAR NO**

- The standard 12 digits numerical.

**MOBILE NO**

- **Sequence**: 10 numerical digits

**IFSC CODE**

- **Example**: PUNB0596600
- **Sequence**: First four alpha, next fifth digit is 0 (zero) always and last six digit is alpha/numeric. Totally 11 digits.

**PIN CODE**

- 6 numerical digits

This Python package is automatically generated by the [OpenAPI Generator](https://openapi-generator.tech) project:

- API version: 1.0.1
- Package version: 1.0.0
- Build package: org.openapitools.codegen.languages.PythonClientCodegen
For more information, please visit [http://credavenue.com](http://credavenue.com)

## Requirements.

Python >= 3.6

## Installation & Usage
### pip install

If the python package is hosted on a repository, you can install directly using:

```sh
pip install git+https://github.com/GIT_USER_ID/GIT_REPO_ID.git
```
(you may need to run `pip` with root permission: `sudo pip install git+https://github.com/GIT_USER_ID/GIT_REPO_ID.git`)

Then import the package:
```python
import colending_python_client
```

### Setuptools

Install via [Setuptools](http://pypi.python.org/pypi/setuptools).

```sh
python setup.py install --user
```
(or `sudo python setup.py install` to install the package for all users)

Then import the package:
```python
import colending_python_client
```

## Getting Started

Please follow the [installation procedure](#installation--usage) and then run the following:

```python

import time
import colending_python_client
from pprint import pprint
from colending_python_client.api import loan_api
from colending_python_client.model.get_payment_response import GetPaymentResponse
from colending_python_client.model.inline_response400 import InlineResponse400
from colending_python_client.model.loan import Loan
# Defining the host is optional and defaults to https://colend-uat-01-api.credavenue.in/colending
# See configuration.py for a list of all supported configuration parameters.
configuration = colending_python_client.Configuration(
    host = "https://colend-uat-01-api.credavenue.in/colending"
)

# The client must configure the authentication and authorization parameters
# in accordance with the API server security policy.
# Examples for each auth method are provided below, use the example that
# satisfies your auth use case.

# Configure API key authorization: api_key
configuration.api_key['api_key'] = 'YOUR_API_KEY'

# Uncomment below to setup prefix (e.g. Bearer) for API key, if needed
# configuration.api_key_prefix['api_key'] = 'Bearer'


# Enter a context with an instance of the API client
with colending_python_client.ApiClient(configuration) as api_client:
    # Create an instance of the API class
    api_instance = loan_api.LoanApi(api_client)
    client_name = "upwards" # str | Name of the client
body = {} # {str: (bool, date, datetime, dict, float, int, list, str, none_type)} | 

    try:
        # Create Loan
        api_response = api_instance.create_loan(client_name, body)
        pprint(api_response)
    except colending_python_client.ApiException as e:
        print("Exception when calling LoanApi->create_loan: %s\n" % e)
```

## Documentation for API Endpoints

All URIs are relative to *https://colend-uat-01-api.credavenue.in/colending*

Class | Method | HTTP request | Description
------------ | ------------- | ------------- | -------------
*LoanApi* | [**create_loan**](docs/LoanApi.md#create_loan) | **POST** /clients/{client_name}/api/v2/loans | Create Loan
*LoanApi* | [**get_loan_details**](docs/LoanApi.md#get_loan_details) | **GET** /clients/{client_name}/api/v2/loans/{loan_id} | Get Loan Details


## Documentation For Models

 - [GetPaymentResponse](docs/GetPaymentResponse.md)
 - [GetPaymentResponseApplicants](docs/GetPaymentResponseApplicants.md)
 - [InlineResponse400](docs/InlineResponse400.md)
 - [InlineResponse400Error](docs/InlineResponse400Error.md)
 - [Loan](docs/Loan.md)


## Documentation For Authorization


## api_key

- **Type**: API key
- **API key parameter name**: api_key
- **Location**: HTTP header


## Author

support@colending.com


## Notes for Large OpenAPI documents
If the OpenAPI document is large, imports in colending_python_client.apis and colending_python_client.models may fail with a
RecursionError indicating the maximum recursion limit has been exceeded. In that case, there are a couple of solutions:

Solution 1:
Use specific imports for apis and models like:
- `from colending_python_client.api.default_api import DefaultApi`
- `from colending_python_client.model.pet import Pet`

Solution 2:
Before importing the package, adjust the maximum recursion limit as shown below:
```
import sys
sys.setrecursionlimit(1500)
import colending_python_client
from colending_python_client.apis import *
from colending_python_client.models import *
```

