We have created access to our Happy Trucker API for you:
 [https://test-happy-trucker-backend.it2media.de/swagger-ui/index.html#/](https://test-happy-trucker-backend.it2media.de/swagger-ui/index.html#/)
1. to use the API, it is necessary to get a time-limited token (5 minutes) with the infoware credentials. To do this, first convert the credentials into a Basic Authentication Base64 string:
- infoware:K2g6z=K8(9>23M#
- aW5mb3dhcmU6SzJnNno9SzgoOT4yM00j

and then get the token:
```bash
curl --location "https://test-happy-trucker-backoffice.it2media.de/oauth2/token" --header "Authorization: Basic aW5mb3dhcmU6SzJnNno9SzgoOT4yM00j" --form "grant_type=client_credentials"
```

```json
{
"access_token":"eyJraWQiOiJhOWQ5NTMzZC1hMGY4LTRmZDItODE1Yy0wZDAwODFjMzQyNjYiLCJhbGciOiJSUzI1NiJ9.eyJzdWIiOiJpbmZvd2FyZSIsImF1ZCI6ImluZm93YXJlIiwibmJmIjoxNzMzNzUxNTEzLCJpc3MiOiJodHRwczovL3Rlc3QtaGFwcHktdHJ1Y2tlci1iYWNrb2ZmaWNlLml0Mm1lZGlhLmRlIiwiZXhwIjoxNzMzNzUxODEzLCJpYXQiOjE3MzM3NTE1MTMsImp0aSI6Ijg4OGIwNzIyLTA2NzMtNDk2Yy05ODkyLWJlMTRlOWQ0MGE5YiJ9.TJxkbzwLK1E6GjiWDRvYnCBeUsnRRcbUoCg3x3t9H4XvUfV4ljCGPY4nTiw910keKGTUX4Mnj5PUyvLvj09dDyPAcNV9tuIPKdB_6HUXaaOFujxt2uqWtdmX2ejbDO9L47sKtQSo7ha0aMpTJzoGXideTA-kn9DcXzS813EqMdB1aBxOwb6yuWI19aAofjp2qLqo8NzPxj31xjCr1zeZqduJsghYaA_ksW6JsoJmpAjlB9K_dPXbKSkcrh7QkBf0me2O4jPAt2AHAVzdeHNDekMUNgvVMYL7RZQygKkQjIlaP8iYi5FoZyFQhi7lsLl1tpAAX2oYlvrfKdLHI6w9XA",
"token_type":"Bearer",
"expires_in":299
}
```