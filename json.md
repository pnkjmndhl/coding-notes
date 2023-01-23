#### example
```js
{
	"first_name": "John",
	"last_name" : "Doe",
	"memberships": ["mem1, mem2"],
	"address": {
			"street": "4 main st",
			"city": "Boston"
			},
	"contacts":[
			{"name": "Brad", "relationship": "friend"}
		]
}
```

##### the above json string define 3 properties- name, age, and car

#### JSON and JavaScript
- syntactically similar to code for creating JavaScript objects
- JavaScript has a builtin function for converting an object into a JSON string, `JSON.parse()`, and back `JSON.stringify()`
- JSON: `{"name":"John"}`, JavaScript: `{name:"John"}`
- JSON values must be string, number, object, array, boolean, or null
- JavaScript, JSON + function, date, or undefined
- accessing values: JavaScript `person["name"]`, or `person.name`
- modifying values: JavaScript `person.name = "Gilbert";`, or, `person["name"] = "Gilbert";`
- JSON is easier and faster than XML