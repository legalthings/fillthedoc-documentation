# Template API

{% api-method method="get" host="https://fillthedoc.com" path="/api/templates" %}
{% api-method-summary %}
Templates
{% endapi-method-summary %}

{% api-method-description %}
Get a list of all published templates.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-query-parameters %}
{% api-method-parameter name="category" type="string" required=false %}
Filter templates on category
{% endapi-method-parameter %}

{% api-method-parameter name="folder" type="string" required=false %}
Get templates from folder and subfolders
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
[
    {
        "id": "welcome",
        "name": "Welcome letter",
        "description": "Welcome letter for new users",
        "categories": [
            "most-used",
            "hr"
        ]
    },
    {
        "id": "labor-agreement",
        "name": "Labor agreement",
        "description": "A labor agreement for temporary or steady employees",
        "categories": [
            "most-used",
            "hr"
        ]
    },
    {
        "id": "cao-employee",
        "name": "CAO Employee",
        "description": "General CAO agreement for employees",
        "categories": [
            "hr"
        ]
    },
    {
        "id": "cao-offshore",
        "name": "CAO Off Shore",
        "description": "CAO agreement for offshore employees",
        "categories": [
            "hr"      
        ]
    },
    {
        "id": "incorporation-bv",
        "name": "Incorporation BV",
        "description": "Offical document for forming a new BV",
        "categories": [
            "most-used",
            "incorporation"
        ]
    },
    {
        "id": "incorporation-holding",
        "name": "Incorporation Holding BV",
        "description": "Official document for forming a new holding BV",
        "categories": [
            "most-used",
            "incorporation"
        ]
    },
    {
        "id": "incorporation-limited-gb",
        "name": "Incorporation Limited (GB)",
        "description": "Official document for forming a British limited",
        "categories": [
            "incorporation"
        ]
    },
    {
        "id": "nda",
        "name": "Non Disclosure Agreement (NDA)",
        "description": "Multi-purpose, one- or two-way NDA",
        "categories": [
            "most-used",
            "hr",
            "sales"
        ]
    },
    {
        "id": "due-diligence",
        "name": "Due diligence report",
        "description": "A due diligence report is request when transfering >10% of the stocks of a company",
        "categories": [
            "sales",
            "takeover"
        ]
    }            
]
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://fillthedoc.com" path="/api/categories" %}
{% api-method-summary %}
Categories
{% endapi-method-summary %}

{% api-method-description %}
Get a list of all categories.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
[
    {
        "id": "most-used",
        "name": "Most used"
    },
    {
        "id": "incorporation",
        "name": "Incorporation"
    },
    {
        "id": "hr",
        "name": "HR agreements"
    },
    {
        "id": "sales",
        "name": "Sales"
    },
    {
        "id": "takeover",
        "name": "Takeover"
    }
]
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

Categories are used to group and filter templates. A template may be part of any number of categories.

{% api-method method="get" host="https://fillthedoc.com" path="/api/folders" %}
{% api-method-summary %}
Folders
{% endapi-method-summary %}

{% api-method-description %}
Get a list of all folder.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
[
    "hr",
    "hr/contracts",
    "hr/dossiers",
    "sales",
    "sales/contracts",
    "sales/offers"
]
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

Templates may be organized in folders. Folders are nested; they may have subfolders.

