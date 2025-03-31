![image](https://github.com/user-attachments/assets/aec831ea-c7ad-4f30-b858-6fb6b98c95d1)![image](https://github.com/user-attachments/assets/6b087a6c-9b0c-483d-910f-7ac45d24dccc)# FamilyNameGenerator

The following Azure Function serves as a sample API that can be called through an Agent in Azure Foundry.

The function itself can return a name from a list if no "name" parameter is given. If a name parameter is given then that is returned.

Pre-requisite:
- .net 8 SDK installed

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

7. In the terminal visi this api-endpoint:
RenderOpenApiDocument: [GET] http://localhost:7120/api/openapi/{version}.{extension}
In my case: http://localhost:7120/api/openapi/v3.json
Save this openapi schema for later.
![image](https://github.com/user-attachments/assets/8d92ec3d-2eac-4b33-adca-7758a7b6caa5)

8. Publish the azure function to Azure
![image](https://github.com/user-attachments/assets/2269d917-8ecd-45e8-9d23-66df58db4837)

9. Navigate to the published Azure Function in Azure
![image](https://github.com/user-attachments/assets/df103cf2-527f-4c22-b697-e68a15233831)

9. Get the Function URL
![image](https://github.com/user-attachments/assets/6dc48bd3-fc0d-4d58-be4f-241e6827cf15)

10. Adjust the openapi schema. Start by update the URL to match the published funcion url, adjust the "requirement" for the input parameter if needed.

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

11. Navigate to the Agent experience in Ai Foundry
![image](https://github.com/user-attachments/assets/058f8847-4bda-4756-be3e-b2fd5435af9f)

12. Create a new Action
![image](https://github.com/user-attachments/assets/880e4e42-77a9-45b5-a3fb-3ce3cdc616df)

13. Paste the openapi schema
![image](https://github.com/user-attachments/assets/0e6b8083-9b51-420a-8269-96b5b9097539)

14. Try it out in the playground,
![image](https://github.com/user-attachments/assets/819547c6-3754-4809-8731-075440217ddc)

15. Prompt the Agent, and it will utilize the API if it finds it relevant.
![image](https://github.com/user-attachments/assets/ab9e924d-ef3f-4afe-bf15-5c81344dd22b)


Additional Resources:
https://thecodeblogger.com/2022/11/03/adding-swagger-page-to-azure-functions-project/
