# Cloud API :
  Send and receive messages using a cloud-hosted version of the WhatsApp Business Platform. The Cloud API, hosted by Meta, allows you to implement WhatsApp Business APIs without the cost of hosting of your own servers and also allows you to more easily scale your business messaging.

 ## Endpoint References : 

 ### Main Root Nodes :

| Node    | Description |
| -------- | ------------|
| /PHONE_NUMBER_ID  | Represents a specific phone number. This endpoint is used to set up   two-factor authentication. |
| /MEDIA_ID | Represents a specific media object. Use this endpoint to get and delete media objects.        |
| /MEDIA_URL    | Represents a specific media URL. Use this endpoint to download media from a URL.        |

### Phone Number ID :
 The /PHONE_NUMBER_ID endpoint has the following edges:

 | Edge                               | Description                                                                                               |
|------------------------------------|-----------------------------------------------------------------------------------------------------------|
| /PHONE_NUMBER_ID/business_compliance_info | Get or update a WhatsApp business phone number's India-based business compliance information.             |
| /PHONE_NUMBER_ID/deregister        | Used to deregister a phone number.                                                                       |
| /PHONE_NUMBER_ID/media             | Used to upload media.                                                                                    |
| /PHONE_NUMBER_ID/messages          | Used to send messages.                                                                                   |
| /PHONE_NUMBER_ID/register          | Used to register a phone number or to migrate WhatsApp Business Accounts from a current On-Premises deployment to the new Cloud-Based API. |
| /PHONE_NUMBER_ID/request_code      | Used to request a code to verify a phone number's ownership.                                             |
| /PHONE_NUMBER_ID/verify_code       | Used to verify a phone number's ownership.                                                               |
| /PHONE_NUMBER_ID/whatsapp_business_profile | Used to get and update a business' profile.                                                        |

# Types of Massages : 
  Use the /PHONE_NUMBER_ID/messages endpoint to send text, media, contacts, location, and interactive messages, as well as message templates to your customers. 

  | Endpoint                          | Authentication                                                                                           |
|-----------------------------------|----------------------------------------------------------------------------------------------------------|
| /PHONE_NUMBER_ID/messages         | Developers can authenticate their API calls with the access token generated in the App Dashboard > WhatsApp > API Setup. Solution Partners must authenticate themselves with an access token with the whatsapp_business_messaging permission. |

Messages are identified by a unique ID (WAMID). You can track message status in the Webhooks through its WAMID. You could also mark an incoming message as read through messages endpoint. This WAMID can have a maximum length of up to 128 characters.

## Text Messages
These are basic text-based messages that businesses can send to their customers. Text messages can contain information, updates, responses to inquiries, or any other text-based communication.
  
  ### example :   
      curl -X  POST \
     'https://graph.facebook.com/v19.0/FROM_PHONE_NUMBER_ID/messages' \
     -H 'Authorization: Bearer ACCESS_TOKEN' \
     -H 'Content-Type: application/json' \
       -d '
     {
      "messaging_product": "whatsapp",
      "recipient_type": "individual",
      "to": "917276363135",
      "type": "text",
      "text": { // the text object
        "preview_url": false,
        "body": "hello i'm from cloud api "
        }
     }'    
          
### Output  : 
   <img src="image1.png" alt="Alt text" >

## Reaction Messages : 
  
In the context of the WhatsApp Business API Cloud, "Reaction Messages" typically refer to messages sent by users in response to specific prompts or actions initiated by the business.

  ### Example :

           curl -X  POST \
     'https://graph.facebook.com/v19.0/FROM_PHONE_NUMBER_ID/messages' \
     -H 'Authorization: Bearer ACCESS_TOKEN' \
     -H 'Content-Type: application/json' \
     -d '{
    "messaging_product": "whatsapp",
    "recipient_type": "individual",
    "to": "917276363135",
    "type": "reaction",
    "reaction": {
    "message_id": "wamid.HBgMOTE3Mjc2MzYzMTM1FQIAERgSQjk0QjU2OTNBOEYzNjAwREVCAA==",
    "emoji": "\uD83D\uDE00"
    }
   }'  

### Output  : 
   <img src="image2.png" alt="Alt text" >

## Media Messages : 

Businesses can also send media-rich messages to their customers, including images, videos, audio files, and documents. These media messages allow businesses to convey information in a visually engaging and interactive manner.   

 ### Example :

           curl -X  POST \
        'https://graph.facebook.com/v19.0/FROM-PHONE-NUMBER-ID/messages' \
        -H 'Authorization: Bearer ACCESS_TOKEN' \
        -H 'Content-Type: application/json' \
        -d '{
          "messaging_product": "whatsapp",
          "recipient_type": "individual",
           "to": "917276363135",
          "type": "image",
          "image": {
            "link": "https://spoonacular.com/cdn/ingredients_100x100/apple.jpg"
               }
              }'

### Output  : 
   <img src="image3.png" alt="Alt text" >    

## Location Messages : 

 Location messages in the context of messaging platforms like WhatsApp refer to messages that include geographical location information. These messages typically allow users to share their current location or a specific location with others.

  ### Example :

           curl -X  POST \
       'https://graph.facebook.com/v19.0/FROM_PHONE_NUMBER_ID/messages' \
       -H 'Authorization: ACCESS_TOKEN' \
       -H 'Content-Type: application/json' \
       -d '{
        "messaging_product": "whatsapp",
         "to": "917276363135",
         "type": "location",
         "location": {
         "longitude": 78.4867,
         "latitude": 17.385,
         "name": "Hyderabad",
         "address": "Hyderabad, Telangana, India"
            }
           }'

  ## Output : 

   <img src="imageLocation.png" alt="Alt text" >  

## Contact Messages :

   In the context of messaging platforms like WhatsApp, contact messages typically refer to messages that include contact information of individuals or businesses. These messages can be sent to share contact details with others quickly and conveniently. Here's how contact messages.

 ### Example :            
                    curl -X  POST \
              'https://graph.facebook.com/v19.0/FROM_PHONE_NUMBER_ID/messages' \
              -H 'Authorization: ACCESS_TOKEN' \
              -H 'Content-Type: application/json' \
                  -d '{
                  "messaging_product": "whatsapp",
                  "to": "917276363135",
                   "type": "contacts",
                    "contacts": [{
                     "addresses": [{
          "street": "STREET",
          "city": "CITY",
          "state": "STATE",
          "zip": "ZIP",
          "country": "COUNTRY",
          "country_code": "COUNTRY_CODE",
          "type": "HOME"
        },
        {
          "street": "STREET",
          "city": "CITY",
          "state": "STATE",
          "zip": "ZIP",
          "country": "COUNTRY",
          "country_code": "COUNTRY_CODE",
          "type": "WORK"
        }],
      "birthday": "1998-01-05",
      "emails": [{
          "email": "EMAIL",
          "type": "WORK"
        },
        {
          "email": "EMAIL",
          "type": "HOME"
        }],
      "name": {
        "formatted_name": "NAME",
        "first_name": "FIRST_NAME",
        "last_name": "LAST_NAME",
        "middle_name": "MIDDLE_NAME",
        "suffix": "SUFFIX",
        "prefix": "PREFIX"
      },
      "org": {
        "company": "COMPANY",
        "department": "DEPARTMENT",
        "title": "TITLE"
      },
      "phones": [{
          "phone": "PHONE_NUMBER",
          "type": "HOME"
        },
        {
          "phone": "PHONE_NUMBER",
          "type": "WORK",
          "wa_id": "PHONE_OR_WA_ID"
        }],
      "urls": [{
          "url": "URL",
          "type": "WORK"
        },
        {
          "url": "URL",
          "type": "HOME"
        }]
    }]
  }'

 ## Output : 

  ![alt text](image5.png)   

## List Messages :

  List Messages on WhatsApp include a menu of up to 10 options. This type of massage offers a simpler and more consistent way for users to make a selection when interacting with your WhatsApp Business Chatbot. These messages have a variety of use cases including Multiple Menu Items & Product Choices.

### Example : 

       {
       "messaging_product": "whatsapp",
       "recipient_type": "individual",
       "to": "917276363135",
       "type": "interactive",
       "interactive": {
       "type": "list",
       "header": {
       "type": "text",
      "text": "HEADER_TEXT"
        },
       "body": {
       "text": "BODY_TEXT"
      },
       "footer": {
       "text": "FOOTER_TEXT"
       },
    "action": {
      "button": "BUTTON_TEXT",
      "sections": [
        {
          "title": "SECTION_1_TITLE",
          "rows": [
            {
              "id": "SECTION_1_ROW_1_ID",
              "title": "SECTION_1_ROW_1_TITLE",
              "description": "SECTION_1_ROW_1_DESCRIPTION"
            },
            {
              "id": "SECTION_1_ROW_2_ID",
              "title": "SECTION_1_ROW_2_TITLE",
              "description": "SECTION_1_ROW_2_DESCRIPTION"
            }
          ]
        },
        {
          "title": "SECTION_2_TITLE",
          "rows": [
            {
              "id": "SECTION_2_ROW_1_ID",
              "title": "SECTION_2_ROW_1_TITLE",
              "description": "SECTION_2_ROW_1_DESCRIPTION"
            },
            {
              "id": "SECTION_2_ROW_2_ID",
              "title": "SECTION_2_ROW_2_TITLE",
              "description": "SECTION_2_ROW_2_DESCRIPTION"
            }
          ]
        }
      ]
    }
       }
       }'

### OutPut :

   <img src="imageList.png" alt="Alt text" >  

## Reply Button :

WhatsApp Interactive Buttons are a part of the WhatsApp API's Message Template offering that allows users to respond using the buttons made available in the message sent by a business.

### Example : 
   
                           {
                    "messaging_product": "whatsapp",
                    "recipient_type":  "individual",
                    "to": "917276363135",
                    "type": "interactive",
                     "interactive": {
                      "type": "button",
                    "body": {
                       "text": "BUTTON_TEXT"
                                 },
                        "action": {
                      "buttons": [
                         {
                         "type": "reply",
                        "reply": {
                          "id": "UNIQUE_BUTTON_ID_1",
                           "title": "BUTTON_TITLE_1"
               }
            },
                         {
          "type": "reply",
          "reply": {
            "id": "UNIQUE_BUTTON_ID_2",
            "title": "BUTTON_TITLE_2"
          }
        }
      ]
    }  
       }
        }

### Output : 

  <img src="imageReplyButton.png" alt="Alt text" > 

## Template Messages :

Template Messages are a crucial feature of the WhatsApp Business API, enabling businesses to send standardized messages to their customers. These messages are pre-approved by WhatsApp and allow for a structured format with placeholders for dynamic content. 

### Example :

    {
     "messaging_product": "whatsapp",
    "recipient_type": "individual",
    "to": "917276363135",
    "type": "template",
    "template": {
    "name": "TEMPLATE_NAME",
    "language": {
      "code": "LANGUAGE_AND_LOCALE_CODE"
    },
    "components": [
      {
        "type": "header",
        "parameters": [
          {
            "type": "image",
            "image": {
              "link": "http(s)://URL"
            }
          }
        ]
      },
      {
        "type": "body",
        "parameters": [
          {
            "type": "text",
            "text": "TEXT_STRING"
          },
          {
            "type": "currency",
            "currency": {
              "fallback_value": "VALUE",
              "code": "USD",
              "amount_1000": NUMBER
            }
          },
          {
            "type": "date_time",
            "date_time": {
              "fallback_value": "MONTH DAY, YEAR"
            }
          }
        ]
      },
      {
        "type": "button",
        "sub_type": "quick_reply",
        "index": "0",
        "parameters": [
          {
            "type": "payload",
            "payload": "PAYLOAD"
          }
        ]
      },
      {
        "type": "button",
        "sub_type": "quick_reply",
        "index": "1",
        "parameters": [
          {
            "type": "payload",
            "payload": "PAYLOAD"
          }
        ]
      }
    ]
    } 
    }

### Output :

## Reply To Message :

In the context of messaging systems like WhatsApp Business API, "Reply To Message" refers to the action of responding to a specific message that has been received from a user or a participant in a conversation. When you reply to a message, your response is typically directed back to the sender of the original message, creating a threaded conversation.

### Example :

      {
     "messaging_product": "whatsapp",
     "context": {
     "message_id": "MESSAGE_ID"
    },
     "to": "917276363135",
     "type": "text",
     "text": {
   
    "body": "Hello! This is your-text-message-content. Replace this text with the actual content you want to send."
      }
     }

### Output :

  <img src="imageReplyToMassage.png" alt="Alt text" > 


## successful response :

A successful response to a message sent via the WhatsApp Business API typically confirms that the message has been successfully delivered to the recipient.

### Example :

               {
      "messaging_product": "whatsapp",
      "contacts": [
        {
          "input": "917276363135",
          "wa_id": "917276363135"
        }
      ],
      "messages": [
        {
          "id":  "wamid.HBgMOTE3Mjc2MzYzMTM1FQIAERgSMEM4NUY1NTIxNTM5MjI1QTY0AA=="
        }
      ]
    }




