
## Templates [/templates/{?category}{?folder}]

+ Parameters
    + category (string, optional) ... Only return templates that are in this category
    + folder (string, optional) ... Only return templates that are in this folder

### List templates [GET]

+ Response 200 (application/json)

        [
            {
                "id": "welcome",
                "name": "Welcome letter",
                "description": "Welcome letter for new users",
                "categories": [
                    "most-used",
                    "hr"
                ],
                "licenses": [
                    "license-1"
                ]
            },
            {
                "id": "labor-agreement",
                "name": "Labor agreement",
                "description": "A labor agreement for temporary or steady employees",
                "categories": [
                    "most-used",
                    "hr"
                ],
                "licenses": [
                    {
                        "id":"license1",
                        "name": "license-1"
                    }
                ]
            },
            {
                "id": "cao-employee",
                "name": "CAO Employee",
                "description": "General CAO agreement for employees",
                "categories": [
                    "hr"
                ],
                "licenses": [
                    {
                        "id":"license1",
                        "name": "license-1"
                    }
                ]
            },
            {
                "id": "cao-offshore",
                "name": "CAO Off Shore",
                "description": "CAO agreement for offshore employees",
                "categories": [
                    "hr"      
                ],
                "licenses": [
                    {
                        "id":"license1",
                        "name": "license-1"
                    }
                ]
            },
            {
                "id": "incorporation-bv",
                "name": "Incorporation BV",
                "description": "Offical document for forming a new BV",
                "categories": [
                    "most-used",
                    "incorporation"
                ],
                "licenses": [
                    {
                        "id":"license1",
                        "name": "license-1"
                    }
                ]
            },
            {
                "id": "incorporation-holding",
                "name": "Incorporation Holding BV",
                "description": "Official document for forming a new holding BV",
                "categories": [
                    "most-used",
                    "incorporation"
                ],
                "licenses": []
            },
            {
                "id": "incorporation-limited-gb",
                "name": "Incorporation Limited (GB)",
                "description": "Official document for forming a British limited",
                "categories": [
                    "incorporation"
                ],
                "licenses": []
            },
            {
                "id": "nda",
                "name": "Non Disclosure Agreement (NDA)",
                "description": "Multi-purpose, one- or two-way NDA",
                "categories": [
                    "most-used",
                    "hr",
                    "sales"
                ],
                "licenses": []
            },
            {
                "id": "due-diligence",
                "name": "Due diligence report",
                "description": "A due diligence report is request when transfering >10% of the stocks of a company",
                "categories": [
                    "sales",
                    "takeover"
                ],
                "licenses": []
            }            
        ]

## Template [/templates/{id}]

+ Parameters
    + id (string)

### Get a template [GET]

+ Response 200 (application/json)

        {
            "id": "welcome",
            "version": 3,
            "name": "Welcome letter",
            "description": "Welcome letter for new users",
            "form": "signup",
            "categories": [
                "most-used",
                "test",
                "hr"
            ],
            "licenses": [
                {
                    "id":"license1",
                    "name": "license-1"
                }
            ]
            "content": "<p>Hello {{ name }}<\/p><p>Welcome to fillthedoc!<\/p><p><br><\/p>"
        }

+ Response 404 (text/plain)


## Categories [/categories/]

Categories are used to group and filter templates. A template may be part of any number of categories.

### Get a list of all categories [GET]
        
+ Response 200 (application/json)

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


# Group Document

Users can create an HTML document based on a template by filling out a form. These documents are stored in fillthedoc and
given a 32 byte unique (unguessable) hash. The document can only be fetched using this hash.

## Documents [/documents/]

### Create a document [POST]

+ Request

        {
            "template": "cao-employee",
            "values": {
                "cao_name": "CAO Employee Pension",
                "pension_fund": "P.A."
            }
        }

+ Response 200 (application/json)

        {
            "id": "3aa4dd6d3d7bfa7d48f686d4f64c6025c73a7057568435e83e566cdb1bf6782a",
            "template": {
                "id": "cao-employee",
                "version": 3
            },
            "values": {
                "cao_name": "CAO Employee Pension",
                "pension_fund": "P.A."
            },
            "content": "<h1>CAO Employee Pension<\/h1><p>The employee falls under the pension arrangement of P.A.<\/p>",
            "created": {
                "user": "367a74cb920b29a664865a21",
                "date": "2014-09-19T14:04:15+0200"
            },
            "last_update": {
                "user": "367a74cb920b29a664865a21",
                "date": "2014-09-19T14:04:15+0200"
            }
        }
        
## Document [/documents/{id}]

Request a document by hash.

+ Parameters
    + id (string) ... The unique, random, unguessable hash

### Get a document [GET]

Use the `Accept` header to specify if you'd like to receive the document including all metadata as JSON or just the contents
as HTML or PDF. Alternatively add a '.json', '.html' or '.pdf' extension to the url. By default the document is returned as JSON.

+ Request

    + Headers
    
            Accept: application/json


+ Response 200 (application/json)

        {
            "id": "3aa4dd6d3d7bfa7d48f686d4f64c6025c73a7057568435e83e566cdb1bf6782a",
            "template": {
                "id": "cao-employee",
                "version": 3
            },
            "values": {
                "cao_name": "CAO Employee Pension",
                "pension_fund": "P.A."
            },
            "content": "<h1>CAO Employee Pension<\/h1><p>The employee falls under the pension arrangement of P.A.<\/p>",
            "created": {
                "user": "367a74cb920b29a664865a21",
                "date": "2014-09-19T14:04:15+0200"
            },
            "last_update": {
                "user": "367a74cb920b29a664865a21",
                "date": "2014-09-19T14:04:15+0200"
            }
        }

+ Response 200 (text/html)

    + Headers

            Last-Modified: Fri, 19 Sep 2014 14:04:15 +0200

    + Body

            <h1>CAO Employee Pension<\/h1><p>The employee falls under the pension arrangement of P.A.<\/p>

+ Response 404

### Update a document [PUT]

Note that you MUST send all values. Missing values are assumed to be `NULL`.

You SHOULD send an `If-Unmodified-Since` header for [optimistic locking](http://en.wikipedia.org/wiki/Optimistic_concurrency_control).
You MAY send back the `last_update` field insted of the header instead.

+ Request

    + Headers

            If-Unmodified-Since: Fri, 19 Sep 2014 14:04:15 +0200

    + Body

            {
                "values": {
                    "cao_name": "CAO Employee Pension",
                    "pension_fund": "P.A."
                }
            }

+ Response 200 (application/json)

        {
            "id": "3aa4dd6d3d7bfa7d48f686d4f64c6025c73a7057568435e83e566cdb1bf6782a",
            "template": {
                "id": "cao-employee",
                "version": 3
            },
            "values": {
                "cao_name": "CAO Employee Pension",
                "pension_fund": "P.A."
            },
            "content": "<h1>CAO Employee Pension<\/h1><p>The employee falls under the pension arrangement of P.A.<\/p>",
            "created": {
                "user": "367a74cb920b29a664865a21",
                "date": "2014-09-19T14:04:15+0200"
            },
            "last_update": {
                "user": "367a74cb920b29a664865a21",
                "date": "2014-09-19T14:04:15+0200"
            }
        }

