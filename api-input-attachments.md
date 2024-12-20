---

copyright:
  years: 2015, 2024
lastupdated: "2024-12-20"

subcollection: watson-assistant


---

{{site.data.keyword.attribute-definition-list}}

# Processing input attachments
{: #api-input-attachments}

If you are building a custom channel application by using the REST API, you can add support for sending media files as input attachments.
{: shortdesc}

The request body of the `message` method supports an `attachments` array, which can specify up to 5 media objects. Media objects that are sent in the `attachments` array can be intercepted and processed by a configured premessage webhook.

For detailed information about how to access attachments by using the API, see the [API reference](/apidocs/assistant-v2#message){: external}.

## Examples
{: #api-input-attachments-examples}

The following example shows the request body that is sent to a premessage webhook with a message body that includes the text `Hello` and a JPEG image file as an attachment. The application that receives the webhook request can parse the `attachments` array and process the attachment, optionally modifying the message, before it is processed by the assistant.

```json
{
  "event":{
    "name":"message_received"
  },
  "options":{
  },
  "payload":{
    "input":{
      "message_type":"text",
      "text":"Hello",
      "source":{
        "type":"user",
        "id":"00000000000000000000000000000000"
      },
      "options":{
        "suggestion_only":false,
        "return_context":true
      },
      "attachments": [
        {
          "media_type": "image/jpeg",
          "url": "https://example.com/yourphoto.jpeg"
        }
      ]
    },
    "context":{
      "global":{
        "system":{
          "user_id":"00000000000000000000000000000000"
        }
      },
      "integrations":{
        "text_messaging":{
          "assistant_phone_number":"+12223334444",
          "private":{
            "user_phone_number":"+14443332222",
            "request_id":"00000000-0000-0000-0000-000000000000",
            "ip_address":"172.10.10.10"
          }
        }
      }
    }
  }
}
```
{: codeblock}

This example shows a stateful `/message` request that is sent by a custom channel application and including a single media attachment.

```javascript
service
  .message({
    assistant_id: '{assistant_id}',
    session_id: '{session_id}',
    input: {
      message_type: 'text',
      text: 'Hello',
      attachments: [
        {
          'media_type': 'image/jpeg',
          'url': 'https://example.com/yourphoto.jpeg'
        }
      ]
    }
  })
  .then(res => {
    console.log(JSON.stringify(res, null, 2));
  })
  .catch(err => {
    console.log(err);
  });
```
{: codeblock}
{: javascript}

```python
response=service.message(
    assistant_id='{assistant_id}',
    session_id='{session_id}',
    input={
        'message_type': 'text',
        'text': 'Hello',
        'attachments': [
            {
                'media_type': 'image/jpeg',
                'url': 'https://example.com/yourphoto.jpeg'
            }
        ]
    }
).get_result()

print(json.dumps(response, indent=2))
```
{: codeblock}
{: python}
