# Ebay\Sell\Feed\ScheduleApi

All URIs are relative to https://api.ebay.com/sell/feed/v1.

Method | HTTP request | Description
------------- | ------------- | -------------
[**createSchedule()**](ScheduleApi.md#createSchedule) | **POST** /schedule | 
[**deleteSchedule()**](ScheduleApi.md#deleteSchedule) | **DELETE** /schedule/{schedule_id} | 
[**getLatestResultFile()**](ScheduleApi.md#getLatestResultFile) | **GET** /schedule/{schedule_id}/download_result_file | 
[**getSchedule()**](ScheduleApi.md#getSchedule) | **GET** /schedule/{schedule_id} | 
[**getScheduleTemplate()**](ScheduleApi.md#getScheduleTemplate) | **GET** /schedule_template/{schedule_template_id} | 
[**getScheduleTemplates()**](ScheduleApi.md#getScheduleTemplates) | **GET** /schedule_template | 
[**getSchedules()**](ScheduleApi.md#getSchedules) | **GET** /schedule | 
[**updateSchedule()**](ScheduleApi.md#updateSchedule) | **PUT** /schedule/{schedule_id} | 


## `createSchedule()`

```php
createSchedule($body): object
```



This method creates a schedule, which is a subscription to the specified schedule template. A schedule periodically generates a report for the feedType specified by the template. Specify the same feedType as the feedType of the associated schedule template. When creating the schedule, if available from the template, you can specify a preferred trigger hour, day of the week, or day of the month. These and other fields are conditionally available as specified by the template. Note: Make sure to include all fields required by the schedule template (scheduleTemplateId). Call the getScheduleTemplate method (or the getScheduleTemplates method), to find out which fields are required or optional. If a field is optional and a default value is provided by the template, the default value will be used if omitted from the payload.A successful call returns the location response header containing the getSchedule call URI to retrieve the schedule you just created. The URL includes the eBay-assigned schedule ID, which you can use to reference the schedule task. To retrieve the details of the create schedule task, use the getSchedule method for a single schedule ID or the getSchedules method to retrieve all schedule details for the specified feed_type. The number of schedules for each feedType is limited. Error code 160031 is returned when you have reached this maximum. Note: Except for schedules with a HALF-HOUR frequency, all schedules will ideally run at the start of each hour ('00' minutes). Actual start time may vary time may vary due to load and other factors.

### Example

```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');


// Configure OAuth2 access token for authorization: Authorization Code
$config = Ebay\Sell\Feed\Configuration::getDefaultConfiguration()->setAccessToken('YOUR_ACCESS_TOKEN');


$apiInstance = new Ebay\Sell\Feed\Api\ScheduleApi(
    // If you want use custom http client, pass your client which implements `GuzzleHttp\ClientInterface`.
    // This is optional, `GuzzleHttp\Client` will be used as default.
    new GuzzleHttp\Client(),
    $config
);
$body = new \Ebay\Sell\Feed\Model\CreateUserScheduleRequest(); // \Ebay\Sell\Feed\Model\CreateUserScheduleRequest | In the request payload: feedType and scheduleTemplateId are required; scheduleName is optional; preferredTriggerHour, preferredTriggerDayOfWeek, preferredTriggerDayOfMonth, scheduleStartDate, scheduleEndDate, and schemaVersion are conditional.

try {
    $result = $apiInstance->createSchedule($body);
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling ScheduleApi->createSchedule: ', $e->getMessage(), PHP_EOL;
}
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **body** | [**\Ebay\Sell\Feed\Model\CreateUserScheduleRequest**](../Model/CreateUserScheduleRequest.md)| In the request payload: feedType and scheduleTemplateId are required; scheduleName is optional; preferredTriggerHour, preferredTriggerDayOfWeek, preferredTriggerDayOfMonth, scheduleStartDate, scheduleEndDate, and schemaVersion are conditional. |

### Return type

**object**

### Authorization

[Authorization Code](../../README.md#Authorization Code)

### HTTP request headers

- **Content-Type**: `application/json`
- **Accept**: `*/*`

[[Back to top]](#) [[Back to API list]](../../README.md#endpoints)
[[Back to Model list]](../../README.md#models)
[[Back to README]](../../README.md)

## `deleteSchedule()`

```php
deleteSchedule($schedule_id)
```



This method deletes an existing schedule. Specify the schedule to delete using the schedule_id path parameter.

### Example

```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');


// Configure OAuth2 access token for authorization: Authorization Code
$config = Ebay\Sell\Feed\Configuration::getDefaultConfiguration()->setAccessToken('YOUR_ACCESS_TOKEN');


$apiInstance = new Ebay\Sell\Feed\Api\ScheduleApi(
    // If you want use custom http client, pass your client which implements `GuzzleHttp\ClientInterface`.
    // This is optional, `GuzzleHttp\Client` will be used as default.
    new GuzzleHttp\Client(),
    $config
);
$schedule_id = 'schedule_id_example'; // string | The schedule_id of the schedule to delete. This ID was generated when the task was created. If you do not know the schedule_id, use the getSchedules method to return all schedules based on a specified feed_type and find the schedule_id of the schedule to delete.

try {
    $apiInstance->deleteSchedule($schedule_id);
} catch (Exception $e) {
    echo 'Exception when calling ScheduleApi->deleteSchedule: ', $e->getMessage(), PHP_EOL;
}
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **schedule_id** | **string**| The schedule_id of the schedule to delete. This ID was generated when the task was created. If you do not know the schedule_id, use the getSchedules method to return all schedules based on a specified feed_type and find the schedule_id of the schedule to delete. |

### Return type

void (empty response body)

### Authorization

[Authorization Code](../../README.md#Authorization Code)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: Not defined

[[Back to top]](#) [[Back to API list]](../../README.md#endpoints)
[[Back to Model list]](../../README.md#models)
[[Back to README]](../../README.md)

## `getLatestResultFile()`

```php
getLatestResultFile($schedule_id): object
```



This method downloads the latest result file generated by the schedule. The response of this call is a compressed or uncompressed CSV, XML, or JSON file, with the applicable file extension (for example: csv.gz). Specify the schedule_id path parameter to download its last generated file.

### Example

```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');


// Configure OAuth2 access token for authorization: Authorization Code
$config = Ebay\Sell\Feed\Configuration::getDefaultConfiguration()->setAccessToken('YOUR_ACCESS_TOKEN');


$apiInstance = new Ebay\Sell\Feed\Api\ScheduleApi(
    // If you want use custom http client, pass your client which implements `GuzzleHttp\ClientInterface`.
    // This is optional, `GuzzleHttp\Client` will be used as default.
    new GuzzleHttp\Client(),
    $config
);
$schedule_id = 'schedule_id_example'; // string | The ID of the schedule for which to retrieve the latest result file. This ID is generated when the schedule was created by the createSchedule method.

try {
    $result = $apiInstance->getLatestResultFile($schedule_id);
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling ScheduleApi->getLatestResultFile: ', $e->getMessage(), PHP_EOL;
}
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **schedule_id** | **string**| The ID of the schedule for which to retrieve the latest result file. This ID is generated when the schedule was created by the createSchedule method. |

### Return type

**object**

### Authorization

[Authorization Code](../../README.md#Authorization Code)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/octet-stream`

[[Back to top]](#) [[Back to API list]](../../README.md#endpoints)
[[Back to Model list]](../../README.md#models)
[[Back to README]](../../README.md)

## `getSchedule()`

```php
getSchedule($schedule_id): \Ebay\Sell\Feed\Model\UserScheduleResponse
```



This method retrieves schedule details and status of the specified schedule. Specify the schedule to retrieve using the schedule_id. Use the getSchedules method to find a schedule if you do not know the schedule_id.

### Example

```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');


// Configure OAuth2 access token for authorization: Authorization Code
$config = Ebay\Sell\Feed\Configuration::getDefaultConfiguration()->setAccessToken('YOUR_ACCESS_TOKEN');


$apiInstance = new Ebay\Sell\Feed\Api\ScheduleApi(
    // If you want use custom http client, pass your client which implements `GuzzleHttp\ClientInterface`.
    // This is optional, `GuzzleHttp\Client` will be used as default.
    new GuzzleHttp\Client(),
    $config
);
$schedule_id = 'schedule_id_example'; // string | The ID of the schedule for which to retrieve the details. This ID is generated when the schedule was created by the createSchedule method.

try {
    $result = $apiInstance->getSchedule($schedule_id);
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling ScheduleApi->getSchedule: ', $e->getMessage(), PHP_EOL;
}
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **schedule_id** | **string**| The ID of the schedule for which to retrieve the details. This ID is generated when the schedule was created by the createSchedule method. |

### Return type

[**\Ebay\Sell\Feed\Model\UserScheduleResponse**](../Model/UserScheduleResponse.md)

### Authorization

[Authorization Code](../../README.md#Authorization Code)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`

[[Back to top]](#) [[Back to API list]](../../README.md#endpoints)
[[Back to Model list]](../../README.md#models)
[[Back to README]](../../README.md)

## `getScheduleTemplate()`

```php
getScheduleTemplate($schedule_template_id): \Ebay\Sell\Feed\Model\ScheduleTemplateResponse
```



This method retrieves the details of the specified template. Specify the template to retrieve using the schedule_template_id path parameter. Use the getScheduleTemplates method to find a schedule template if you do not know the schedule_template_id.

### Example

```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');


// Configure OAuth2 access token for authorization: Authorization Code
$config = Ebay\Sell\Feed\Configuration::getDefaultConfiguration()->setAccessToken('YOUR_ACCESS_TOKEN');


$apiInstance = new Ebay\Sell\Feed\Api\ScheduleApi(
    // If you want use custom http client, pass your client which implements `GuzzleHttp\ClientInterface`.
    // This is optional, `GuzzleHttp\Client` will be used as default.
    new GuzzleHttp\Client(),
    $config
);
$schedule_template_id = 'schedule_template_id_example'; // string | The ID of the template to retrieve. If you do not know the schedule_template_id, refer to the documentation or use the getScheduleTemplates method to find the available schedule templates.

try {
    $result = $apiInstance->getScheduleTemplate($schedule_template_id);
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling ScheduleApi->getScheduleTemplate: ', $e->getMessage(), PHP_EOL;
}
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **schedule_template_id** | **string**| The ID of the template to retrieve. If you do not know the schedule_template_id, refer to the documentation or use the getScheduleTemplates method to find the available schedule templates. |

### Return type

[**\Ebay\Sell\Feed\Model\ScheduleTemplateResponse**](../Model/ScheduleTemplateResponse.md)

### Authorization

[Authorization Code](../../README.md#Authorization Code)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`

[[Back to top]](#) [[Back to API list]](../../README.md#endpoints)
[[Back to Model list]](../../README.md#models)
[[Back to README]](../../README.md)

## `getScheduleTemplates()`

```php
getScheduleTemplates($feed_type, $limit, $offset): \Ebay\Sell\Feed\Model\ScheduleTemplateCollection
```



This method retrieves an array containing the details and status of all schedule templates based on the specified feed_type. Use this method to find a schedule template if you do not know the schedule_template_id.

### Example

```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');


// Configure OAuth2 access token for authorization: Authorization Code
$config = Ebay\Sell\Feed\Configuration::getDefaultConfiguration()->setAccessToken('YOUR_ACCESS_TOKEN');


$apiInstance = new Ebay\Sell\Feed\Api\ScheduleApi(
    // If you want use custom http client, pass your client which implements `GuzzleHttp\ClientInterface`.
    // This is optional, `GuzzleHttp\Client` will be used as default.
    new GuzzleHttp\Client(),
    $config
);
$feed_type = 'feed_type_example'; // string | The feed type of the schedule templates to retrieve.
$limit = 56; // int | The maximum number of schedule templates that can be returned on each page of the paginated response. Use this parameter in conjunction with the offset parameter to control the pagination of the output. Note: This feature employs a zero-based list, where the first item in the list has an offset of 0. For example, if offset is set to 10 and limit is set to 10, the call retrieves schedule templates 11 thru 20 from the result set. If this parameter is omitted, the default value is used. Default: 10 Maximum: 500
$offset = 56; // int | The number of schedule templates to skip in the result set before returning the first template in the paginated response. Combine offset with the limit query parameter to control the items returned in the response. For example, if you supply an offset of 0 and a limit of 10, the first page of the response contains the first 10 items from the complete list of items retrieved by the call. If offset is 10 and limit is 20, the first page of the response contains items 11-30 from the complete result set. If this query parameter is not set, the default value is used and the first page of records is returned. Default: 0

try {
    $result = $apiInstance->getScheduleTemplates($feed_type, $limit, $offset);
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling ScheduleApi->getScheduleTemplates: ', $e->getMessage(), PHP_EOL;
}
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **feed_type** | **string**| The feed type of the schedule templates to retrieve. |
 **limit** | **int**| The maximum number of schedule templates that can be returned on each page of the paginated response. Use this parameter in conjunction with the offset parameter to control the pagination of the output. Note: This feature employs a zero-based list, where the first item in the list has an offset of 0. For example, if offset is set to 10 and limit is set to 10, the call retrieves schedule templates 11 thru 20 from the result set. If this parameter is omitted, the default value is used. Default: 10 Maximum: 500 | [optional]
 **offset** | **int**| The number of schedule templates to skip in the result set before returning the first template in the paginated response. Combine offset with the limit query parameter to control the items returned in the response. For example, if you supply an offset of 0 and a limit of 10, the first page of the response contains the first 10 items from the complete list of items retrieved by the call. If offset is 10 and limit is 20, the first page of the response contains items 11-30 from the complete result set. If this query parameter is not set, the default value is used and the first page of records is returned. Default: 0 | [optional]

### Return type

[**\Ebay\Sell\Feed\Model\ScheduleTemplateCollection**](../Model/ScheduleTemplateCollection.md)

### Authorization

[Authorization Code](../../README.md#Authorization Code)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`

[[Back to top]](#) [[Back to API list]](../../README.md#endpoints)
[[Back to Model list]](../../README.md#models)
[[Back to README]](../../README.md)

## `getSchedules()`

```php
getSchedules($feed_type, $limit, $offset): \Ebay\Sell\Feed\Model\UserScheduleCollection
```



This method retrieves an array containing the details and status of all schedules based on the specified feed_type. Use this method to find a schedule if you do not know the schedule_id.

### Example

```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');


// Configure OAuth2 access token for authorization: Authorization Code
$config = Ebay\Sell\Feed\Configuration::getDefaultConfiguration()->setAccessToken('YOUR_ACCESS_TOKEN');


$apiInstance = new Ebay\Sell\Feed\Api\ScheduleApi(
    // If you want use custom http client, pass your client which implements `GuzzleHttp\ClientInterface`.
    // This is optional, `GuzzleHttp\Client` will be used as default.
    new GuzzleHttp\Client(),
    $config
);
$feed_type = 'feed_type_example'; // string | The feedType associated with the schedule.
$limit = 56; // int | The maximum number of schedules that can be returned on each page of the paginated response. Use this parameter in conjunction with the offset parameter to control the pagination of the output. Note: This feature employs a zero-based list, where the first item in the list has an offset of 0. For example, if offset is set to 10 and limit is set to 10, the call retrieves schedules 11 thru 20 from the result set. If this parameter is omitted, the default value is used. Default: 10 Maximum: 500
$offset = 56; // int | The number of schedules to skip in the result set before returning the first schedule in the paginated response. Combine offset with the limit query parameter to control the items returned in the response. For example, if you supply an offset of 0 and a limit of 10, the first page of the response contains the first 10 items from the complete list of items retrieved by the call. If offset is 10 and limit is 20, the first page of the response contains items 11-30 from the complete result set. If this query parameter is not set, the default value is used and the first page of records is returned. Default: 0

try {
    $result = $apiInstance->getSchedules($feed_type, $limit, $offset);
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling ScheduleApi->getSchedules: ', $e->getMessage(), PHP_EOL;
}
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **feed_type** | **string**| The feedType associated with the schedule. |
 **limit** | **int**| The maximum number of schedules that can be returned on each page of the paginated response. Use this parameter in conjunction with the offset parameter to control the pagination of the output. Note: This feature employs a zero-based list, where the first item in the list has an offset of 0. For example, if offset is set to 10 and limit is set to 10, the call retrieves schedules 11 thru 20 from the result set. If this parameter is omitted, the default value is used. Default: 10 Maximum: 500 | [optional]
 **offset** | **int**| The number of schedules to skip in the result set before returning the first schedule in the paginated response. Combine offset with the limit query parameter to control the items returned in the response. For example, if you supply an offset of 0 and a limit of 10, the first page of the response contains the first 10 items from the complete list of items retrieved by the call. If offset is 10 and limit is 20, the first page of the response contains items 11-30 from the complete result set. If this query parameter is not set, the default value is used and the first page of records is returned. Default: 0 | [optional]

### Return type

[**\Ebay\Sell\Feed\Model\UserScheduleCollection**](../Model/UserScheduleCollection.md)

### Authorization

[Authorization Code](../../README.md#Authorization Code)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`

[[Back to top]](#) [[Back to API list]](../../README.md#endpoints)
[[Back to Model list]](../../README.md#models)
[[Back to README]](../../README.md)

## `updateSchedule()`

```php
updateSchedule($schedule_id, $body)
```



This method updates an existing schedule. Specify the schedule to update using the schedule_id path parameter. If the schedule template has changed after the schedule was created or updated, the input will be validated using the changed template. Note: Make sure to include all fields required by the schedule template (scheduleTemplateId). Call the getScheduleTemplate method (or the getScheduleTemplates method), to find out which fields are required or optional. If you do not know the scheduleTemplateId, call the getSchedule method to find out.

### Example

```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');


// Configure OAuth2 access token for authorization: Authorization Code
$config = Ebay\Sell\Feed\Configuration::getDefaultConfiguration()->setAccessToken('YOUR_ACCESS_TOKEN');


$apiInstance = new Ebay\Sell\Feed\Api\ScheduleApi(
    // If you want use custom http client, pass your client which implements `GuzzleHttp\ClientInterface`.
    // This is optional, `GuzzleHttp\Client` will be used as default.
    new GuzzleHttp\Client(),
    $config
);
$schedule_id = 'schedule_id_example'; // string | The ID of the schedule to update. This ID is generated when the schedule was created by the createSchedule method.
$body = new \Ebay\Sell\Feed\Model\UpdateUserScheduleRequest(); // \Ebay\Sell\Feed\Model\UpdateUserScheduleRequest | In the request payload: scheduleName is optional; preferredTriggerHour, preferredTriggerDayOfWeek, preferredTriggerDayOfMonth, scheduleStartDate, scheduleEndDate, and schemaVersion are conditional.

try {
    $apiInstance->updateSchedule($schedule_id, $body);
} catch (Exception $e) {
    echo 'Exception when calling ScheduleApi->updateSchedule: ', $e->getMessage(), PHP_EOL;
}
```

### Parameters

Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **schedule_id** | **string**| The ID of the schedule to update. This ID is generated when the schedule was created by the createSchedule method. |
 **body** | [**\Ebay\Sell\Feed\Model\UpdateUserScheduleRequest**](../Model/UpdateUserScheduleRequest.md)| In the request payload: scheduleName is optional; preferredTriggerHour, preferredTriggerDayOfWeek, preferredTriggerDayOfMonth, scheduleStartDate, scheduleEndDate, and schemaVersion are conditional. |

### Return type

void (empty response body)

### Authorization

[Authorization Code](../../README.md#Authorization Code)

### HTTP request headers

- **Content-Type**: `application/json`
- **Accept**: Not defined

[[Back to top]](#) [[Back to API list]](../../README.md#endpoints)
[[Back to Model list]](../../README.md#models)
[[Back to README]](../../README.md)
