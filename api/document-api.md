# Document API

Users can create a document based on a template by filling out a form. These documents are stored by fillthedoc and given a 32 byte unique \(unguessable\) hash as identifier. The document can only be fetched using this hash as JSON data, HTML or PDF.

{% api-method method="post" host="https://fillthedoc.com" path="/api/documents" %}
{% api-method-summary %}
Create a document
{% endapi-method-summary %}

{% api-method-description %}
Create a new document based on a template.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="template" type="string" required=true %}
Template id or reference
{% endapi-method-parameter %}

{% api-method-parameter name="values" type="object" required=false %}
Data to prefill the document
{% endapi-method-parameter %}

{% api-method-parameter name="callback" type="string" required=false %}
Webhook URL that's called when the document is filled out
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=100 %}
{% api-method-response-example-description %}
Example request
{% endapi-method-response-example-description %}

```javascript
{
    "template": "cao-employee",
    "values": {
        "cao_name": "CAO Employee Pension",
        "pension_fund": "P.A."
    }
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
    "id": "o00wocs44sksk0008kw0kc08cwcs0s8sc0k8owgggc0g0os8swg400c00gc8cosg",
    "template": {
        "version": "2019-08-19T22:07:51",
        "id": "43448bea-42ad-4c68-9962-2475bec7ecec",
        "reference": "cao-employee",
        "published": true,
        "name": "CAO Employee",
        "description": "CAO for employees in the IT industry",
        "categories": [],
        "folder": "hr/contracts",
        "disclaimer": "",
        "locale": "nl_NL",
        "section": "",
        "last_modified": {
            "user": null,
            "date": "2019-08-19T22:07:51+00:00",
            "etag": null
        },
        "import_master_date": null,
        "type": "template"
    },
    "values": {
        "cao_name": "CAO Employee Pension",
        "pension_fund": "P.A."
    },
    "created": {
        "user_id": "a29bf252685445cdc66e1be76403304a296645e7e1d5cf27ff5c7cb8cf4d7c00",
        "date": "2019-08-27T00:52:10+00:00"
    },
    "locale": "nl_NL",
    "step": null,
    "edit_url": "http://localhost/legalthings/o00wocs44sksk0008kw0kc08cwcs0s8sc0k8owgggc0g0os8swg400c00gc8cosg"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

The `template` property is required and can be a template id or template reference. When creating a new document, the latest version of the template is always used. Only published templates can be used to create a document.

The document can be prefilled by adding a `values` property in the request. The data should match the structure defined by the template's form.

The response contains an `edit_url` property. If the end user needs to complete the information for the document, send him to this URL. The document id is a unique and unguessable 32 bit random value. The user doesn't need any information other than this URL.

If a `callback` URL was specified when creating the document, it will be called when the end user completes filling out the document. The request body is a JSON representation of the document and similar to the response body when creating a document.

The document will automatically be locked after the user has completed the form. You may update the document to unlock it.

{% api-method method="get" host="https://fillthedoc.com" path="/api/documents/{id}" %}
{% api-method-summary %}
Retrieve a document
{% endapi-method-summary %}

{% api-method-description %}
Get a document as PDF, HTML or JSON.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
Unique \(32 bit\) document id
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Accept" type="string" required=false %}
"application/pdf", "text/html" or "application/json"
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
    "id": "o00wocs44sksk0008kw0kc08cwcs0s8sc0k8owgggc0g0os8swg400c00gc8cosg",
    "template": {
        "version": "2019-08-19T22:07:51",
        "id": "43448bea-42ad-4c68-9962-2475bec7ecec",
        "reference": "cao-employee",
        "published": true,
        "name": "CAO Employee",
        "description": "CAO for employees in the IT industry",
        "categories": [],
        "folder": "hr/contracts",
        "disclaimer": "",
        "locale": "nl_NL",
        "section": "",
        "last_modified": {
            "user": null,
            "date": "2019-08-19T22:07:51+00:00",
            "etag": null
        },
        "import_master_date": null,
        "type": "template"
    },
    "values": {
        "cao_name": "CAO Employee Pension",
        "pension_fund": "P.A.",
        "first_name": "John",
        "last_name": "Doe",
        "address": "Dam 1",
        "postalcode": "1012JS",
        "city": "Amsterdam"
    },
    "created": {
        "user_id": "a29bf252685445cdc66e1be76403304a296645e7e1d5cf27ff5c7cb8cf4d7c00",
        "date": "2019-08-27T00:52:10+00:00"
    },
    "last_update": {
        "user": null,
        "date": "2019-08-27T00:59:21+00:00"
    },
    "locale": "nl_NL",
    "step": "finished"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

Use the `Accept` header to specify if you'd like to receive the document data and metadata as JSON or just contents as PDF or HTML.

Do not send the URL for generating the PDF directly to the end user. It will not be accessible without the API key. Instead, use the API to download the PDF, store it locally, and allow the user to download it from your system.

{% api-method method="post" host="https://fillthedoc.com" path="/api/documents/{id}" %}
{% api-method-summary %}
Update a document
{% endapi-method-summary %}

{% api-method-description %}
Update the document data or unlock the document.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
Unique \(32 bit\) document id
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="If-Unmodified-Since" type="string" required=false %}
Used for optimistic locking
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="step" type="string" required=false %}
Step the user is on or "finished" when done
{% endapi-method-parameter %}

{% api-method-parameter name="values" type="object" required=false %}
Data of the document
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=100 %}
{% api-method-response-example-description %}
Request example
{% endapi-method-response-example-description %}

```javascript
{
    "step": null,
    "values": {
        "country": "Netherlands"
    }
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
    "id": "o00wocs44sksk0008kw0kc08cwcs0s8sc0k8owgggc0g0os8swg400c00gc8cosg",
    "template": {
        "version": "2019-08-19T22:07:51",
        "id": "43448bea-42ad-4c68-9962-2475bec7ecec",
        "reference": "cao-employee",
        "published": true,
        "name": "CAO Employee",
        "description": "CAO for employees in the IT industry",
        "categories": [],
        "folder": "hr/contracts",
        "disclaimer": "",
        "locale": "nl_NL",
        "section": "",
        "last_modified": {
            "user": null,
            "date": "2019-08-19T22:07:51+00:00",
            "etag": null
        },
        "import_master_date": null,
        "type": "template"
    },
    "values": {
        "cao_name": "CAO Employee Pension",
        "pension_fund": "P.A.",
        "first_name": "John",
        "last_name": "Doe",
        "address": "Dam 1",
        "postalcode": "1012JS",
        "city": "Amsterdam",
        "country": "Netherlands"
    },
    "created": {
        "user_id": "a29bf252685445cdc66e1be76403304a296645e7e1d5cf27ff5c7cb8cf4d7c00",
        "date": "2019-08-27T00:52:10+00:00"
    },
    "last_update": {
        "user": "a29bf252685445cdc66e1be76403304a296645e7e1d5cf27ff5c7cb8cf4d7c00",
        "date": "2019-08-27T01:03:52+00:00"
    },
    "locale": "nl_NL",
    "step": null,
    "edit_url": "http://localhost/legalthings/o00wocs44sksk0008kw0kc08cwcs0s8sc0k8owgggc0g0os8swg400c00gc8cosg"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

Documents are automatically be locked after the user has completed the form. This is indicated by the `step` property which is set to `finished`. Set the `step` property to `null` to allow the user to modify the document. The edit url remains unchanged. Once the end user is finished, the webhook \(specified as `callback` when the document was created\) will be called again.

It's possible to modify the data, prior to generating the PDF or HTML document, via the `values` property. The values are merged, even for nested data, as specified by [RFC 7396](https://tools.ietf.org/html/rfc7396) _\(regardless of the `Content-Type`\)_.

You should send an `If-Unmodified-Since` header for [optimistic locking](http://en.wikipedia.org/wiki/Optimistic_concurrency_control). This prevents overwriting the document data, which may have been modified by the user is the document is not locked.

{% api-method method="delete" host="https://fillthedoc.com" path="/api/documents/{id}" %}
{% api-method-summary %}
Delete a document
{% endapi-method-summary %}

{% api-method-description %}
Delete a document from fillthedoc.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
Unique \(32 bit\) document id
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=204 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```text

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

