### **What is google fci?**
	- Firebase Cloud Message api.
	- [docs](https://firebase.google.com/docs/reference/fcm/rest)
	- [client libs](https://docs.cloud.google.com/apis/docs/client-libraries-explained)
	- [ap reference](https://firebase.google.com/docs/reference/fcm/rest/v1/projects.messages)

```json
{
	// general json schema.
	"name": string,
	"data": {
		string: string
	},
	"notification": {
		object: (Notification)
	},
	"android": {
		object: (Android config)
	},
	"webpush": {
		object: (WebpushConfig)
	},
	"apns": {
		object: (ApnsConfig)
	},
	"fcm_options": {
		object: (FcmOptions)
	},
	 // Union field `target` can be only one of the following:
	"token": string,
	"fid": string,
	"topic": string,
	"condition": string
	// End of list of possible types for union field `target`.
}
```

```json
{
	// Notification
	"title": string,
	"body": string,
	"image": string // url of an image to be downloaded and displayed. (JPEG, PNG, BMP), GIF and video only works on IOS, Android has 1MB size limit.
}
```
```json
{
	//Android config
	"collapse_key": string, // id of a group of messages that can be collapsed
	"priority": enum, // NORMAL, or HIGH
	"ttl": string, // seconds the message should be kept in fcm storage. max 4 weeks, 0 means send immediatly.
	"restriceted_package_name"
	...
}
```

```json
{
	
}
```