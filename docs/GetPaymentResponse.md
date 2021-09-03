# GetPaymentResponse


## Properties
Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**client_loan_id** | **str** | Unique identifier for the loan | [optional] 
**product_id** | **int** | Product ID | [optional] 
**principal_amount** | **float** | Principal amount for the loan | [optional] 
**interest_rate** | **float** | Interest rate in percentage | [optional] 
**tenure** | **int** | Tenure of the loan | [optional] 
**tenure_frequency** | **str** | Tenure Frequency | [optional] 
**no_of_repayments** | **int** | Number of Repayments | [optional] 
**status** | **str** | Current status of the loan | [optional] 
**principal_outstanding** | **float** | current POS of the loan | [optional] 
**reject_reason** | **str, none_type** | Reason for rejecting loan | [optional] 
**applicants** | [**[GetPaymentResponseApplicants]**](GetPaymentResponseApplicants.md) | Array of applicant details | [optional] 
**any string name** | **bool, date, datetime, dict, float, int, list, str, none_type** | any string name can be used but the value must be the correct type | [optional]

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


