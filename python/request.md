```py
response = requests.get(baseUrl, params = parameters)
url = respose.url
content = response.content
info = json.loads(content)
```