# Azure Function Sample API for Azure Foundry Agent
This repository contains an Azure Function that serves as a sample API, designed to be called through an Agent in Azure Foundry. The function demonstrates how to integrate Azure Functions with Azure Foundry, providing a practical example for developers.

## Features
* Sample API Endpoint: A simple API endpoint that can be invoked by an Agent in Azure Foundry.
* Integration with Azure Foundry: Demonstrates how to set up and configure the Azure Function to work seamlessly with Azure Foundry.
* Scalable and Serverless: Leverages the power of Azure Functions to provide a scalable and serverless solution.
* Easy to Deploy: Includes deployment scripts and instructions to help you get started quickly

## Azure Function: FamilyNameGenerator
This C# code defines an Azure Function named FamilyNameGenerator. When the function is triggered via an HTTP request, it will return a personalized greeting if a "name" is provided as input parameter, or a random family name if not.

## Pre-requisite:
- .net 8 SDK installed

## Tutorial
Below tutorial will show you how to create the azure function from Visual studio, or you can just clone this project:

1. Create a new project:
![image](https://github.com/user-attachments/assets/b93d3b87-95a6-4dee-93d4-efbecac5798c)

2. Choose the Azure Function template:
![image](https://github.com/user-attachments/assets/e664e418-3b42-43fa-bfa6-73ace4031265)

3. Give solution a name and folder to store solution:
![image](https://github.com/user-attachments/assets/1a8cc9df-3323-4f7a-a4f2-adc5c1b19f72)

4. Additional config: 
Function worker: .Net 8 LTS, Function: Http trigger with OpenAPI
![image](https://github.com/user-attachments/assets/b2b65149-00cd-4b86-8ce2-b7c13f6d75c1)

5. Test and Verify the solution by Pressing F5 to debug the solution locally
![image](https://github.com/user-attachments/assets/5dd53f4b-ed64-44e9-994e-71f3e1e29989)

6. Customize the code to your liking, and debug it once again.

7. In the terminal visit this api-endpoint:
![image](https://github.com/user-attachments/assets/b6378cc0-80e3-4720-b3c2-662598d455ed)

* RenderOpenApiDocument: [GET] http://localhost:7120/api/openapi/{version}.{extension}
* In my case: http://localhost:7120/api/openapi/v3.json

8. Save this openapi schema for later.
![image](https://github.com/user-attachments/assets/8d92ec3d-2eac-4b33-adca-7758a7b6caa5)

9. Publish the azure function to Azure
![image](https://github.com/user-attachments/assets/2269d917-8ecd-45e8-9d23-66df58db4837)

10. Navigate to the published Azure Function in Azure
![image](https://github.com/user-attachments/assets/df103cf2-527f-4c22-b697-e68a15233831)

11. Get the Function URL
![image](https://github.com/user-attachments/assets/6dc48bd3-fc0d-4d58-be4f-241e6827cf15)

12. Adjust the openapi schema. Start by update the URL to match the published funcion url, adjust the "requirement" for the input parameter if needed.

```
{
  "openapi": "3.0.1",
  "info": {
    "title": "OpenAPI Document on Azure Functions",
    "description": "This is the OpenAPI Document on Azure Functions",
    "version": "1.0.0"
  },
  "servers": [
    {
      "url": "https://lainamegenerator.azurewebsites.net/api/FamilyNameGenerator?"
    }
  ],
  "paths": {
    "/FamilyNameGenerator": {
      "get": {
        "tags": [
          "name"
        ],
        "operationId": "Run",
        "parameters": [
          {
            "name": "name",
            "in": "query",
            "description": "you can optionally provide a name of a person",
            "required": false,
            "schema": {
              "type": "string"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "The OK response",
            "content": {
              "text/plain": {
                "schema": {
                  "type": "string"
                }
              }
            }
          }
        }
      }
    }
  },
  "components": {}
}
```

13. Navigate to the Agent experience in Ai Foundry
![image](https://github.com/user-attachments/assets/058f8847-4bda-4756-be3e-b2fd5435af9f)

14. Create a new Action
![image](https://github.com/user-attachments/assets/880e4e42-77a9-45b5-a3fb-3ce3cdc616df)

15. Paste the openapi schema
![image](https://github.com/user-attachments/assets/0e6b8083-9b51-420a-8269-96b5b9097539)

16. Try it out in the playground,
![image](https://github.com/user-attachments/assets/819547c6-3754-4809-8731-075440217ddc)

17. Prompt the Agent, and it will utilize the API if it finds it relevant.
![image](https://github.com/user-attachments/assets/ab9e924d-ef3f-4afe-bf15-5c81344dd22b)


Additional Resources:
https://thecodeblogger.com/2022/11/03/adding-swagger-page-to-azure-functions-project/
