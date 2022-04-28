# Datahmac

This extension defines an HMAC hash value computed from the `data`.

If the `datahmac` attribute exists, the receiver should compute the HMAC hash of the received `data` and compare it with the value of the attribute. They MUST be identical.

Both the sender and the receiver MUST agree on a *secret key* and an *algorithm*. Unless specified otherwise, the default algorithm is SHA-512. If a different algorithm is to be used, an additional `datahmacalg` attribute can specify the algorightm.

## Attributes

### datahmac

- Type: `Binary`
- Description: The HMAC hash calculated from the `data` using a *secret key*.
- Constraints:
  - OPTIONAL

### datahmacalg

- Type: `String`
- Description: The algorithm used to calculate the hash
- Default: SHA-512
- Constraints:
  - REQUIRED IF the algorithm used isn't the default

# Examples

An example of a CloudEvent with an HMAC hash (serialized as JSON):

```JSON
{
    "specversion" : "1.0",
    "type" : "com.github.pull_request.opened",
    "source" : "https://github.com/cloudevents/spec/pull/123",
    "id" : "A234-1234-1234",
    "datacontenttype" : "text/xml",
    "data" : "<much wow=\"xml\"/>",
    "datahmac" : "wHGjAG5QirFrg3TxZkJFG1a2Imgf6ybBn+QSFLno/jUNT1rh4QBVEgFbd4QfqrKKrR8Uif6u2XrlLINZWxVE/Q=="
}
```

An example of a CloudEvent with an HMAC hash created with a SHA-256 algorithm (serialized as JSON):

```JSON
{
    "specversion" : "1.0",
    "type" : "com.github.pull_request.opened",
    "source" : "https://github.com/cloudevents/spec/pull/123",
    "id" : "A234-1234-1234",
    "datacontenttype" : "text/xml",
    "data" : "<much wow=\"xml\"/>",
    "datahmac": "0hTrN1y5E3s/gNdjSFaurLnHt3M9tJ6m2IsYTaL+cvc=",
    "datahmacalg": "SHA-256"
}
```
