---
subcategory: "Ingest"
layout: ""
page_title: "Elasticstack: elasticstack_elasticsearch_ingest_processor_append Data Source"
description: |-
  Helper data source to create a processor which appends one or more values to an existing array if the field already exists and it is an array.
---

# Data Source: elasticstack_elasticsearch_ingest_processor_append

Helper data source to which can be used to create a processor to append one or more values to an existing array if the field already exists and it is an array.
Converts a scalar to an array and appends one or more values to it if the field exists and it is a scalar. Creates an array containing the provided values if the field doesn’t exist.

See: https://www.elastic.co/guide/en/elasticsearch/reference/current/append-processor.html

## Example Usage

```terraform
provider "elasticstack" {
  elasticsearch {}
}

data "elasticstack_elasticsearch_ingest_processor_append" "tags" {
  field = "tags"
  value = ["production", "{{{app}}}", "{{{owner}}}"]
}

resource "elasticstack_elasticsearch_ingest_pipeline" "my_ingest_pipeline" {
  name = "append-ingest"

  processors = [
    data.elasticstack_elasticsearch_ingest_processor_append.tags.json
  ]
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- **field** (String) The field to be appended to.
- **value** (List of String) The value to be appended.

### Optional

- **allow_duplicates** (Boolean) If `false`, the processor does not append values already present in the field.
- **description** (String) Description of the processor.
- **if** (String) Conditionally execute the processor
- **ignore_failure** (Boolean) Ignore failures for the processor.
- **media_type** (String) The media type for encoding value. Applies only when value is a template snippet. Must be one of `application/json`, `text/plain`, or `application/x-www-form-urlencoded`.
- **on_failure** (List of String) Handle failures for the processor.
- **tag** (String) Identifier for the processor.

### Read-Only

- **id** (String) Internal identifier of the resource
- **json** (String) JSON representation of this data source.

