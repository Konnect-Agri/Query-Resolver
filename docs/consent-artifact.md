## Consent Artifact
A consent artifact is a document which defines all the entities, parameters, access levels, data restrictions etc for a consent.

A detailed doc on consent artifact can be found [here](https://dla.gov.in/sites/default/files/pdf/MeitY-Consent-Tech-Framework%20v1.1.pdf)


The following json describes the structure of a consent artifact
```
{
    "created": "YYYY-MM-DDThh:mm:ssZn.n",
    "expires": "YYYY-MM-DDThh:mm:ssZn.n",
    "id": ""
    "revocable": false,
    "collector": {
        "id": ""
        "url": "https://sample-collector/api/v1/collect"
    },
    "consumer": {
        "id": "",
        "url": "https://sample-consumer/api/v1/consume"
    },
    "provider": {
        "id": "",
        "url": "https://sample-consumer/api/v1"
    },
    "user": {
        "type": "AADHAAR|MOBILE|PAN|PASSPORT|...",
        "name": "",
        "issuer": "",
        "dpID": "",
        "cmID": "",
        "dcID": ""
    },
    "revoker": {
        "url": "https://sample-revoker/api/v1/revoke",
        "name": "",
        "id": ""
    },
    "purpose": "",
    "user_sign": "",
    "collector_sign": "",
    "log": {
        "consent_use": {
            "url": "https://sample-log/api/v1/log"
        },
        "data_access": {
            "url": "https://sample-log/api/v1/log"
        }
    },
    "data": <Valid superset GraphQL query of consented data>"
}
```


### Query of consent artifact
Query structure of consent artifact is same as [GraphQL Oct 2021 Release](https://spec.graphql.org/October2021/#sec-Overview), we recommend giving it a read since it's cirtical in understanding the consent artifact.


The query param inside a consent artifact defines what data is allowed to be accessed by the consent artifact
We can define this access for every query root to give very fine grained control of the data.

---

Example query to fetch attendances of people of all industries in district "abu" 

```
attendance(where: {industry: {district: {_eq: "abu"}}}) {
    date
    name
    created_at
    industry {
      district
    }
  }
```