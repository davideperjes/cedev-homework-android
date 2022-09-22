# Marvel Character Browser
## Task
Your task will be to create a simple Android mobile application where users can search for Marvel characters based on their names. If the user starts typing into an input field, the app should start fetching the data from the Marvel API and show it to the user in a list.

The list items should display information about the characters, such as their **names**, a **thumbnail** image, and a **description** text, which should be limited in 100 characters.

When the user taps on a character in the list, it should open a web browser with the character's detail URL. (*json response:* `urls.type == "detail"`)

When the user scrolls down in the list, the app should fetch more characters lazily (pagination).

## API

Documentation: https://developer.marvel.com/documentation/generalinfo

### Character endpoint

* Base URL: **https://gateway.marvel.com**
* Characters endpoint: **/v1/public/characters**
* Search param: **?nameStartsWith={q}** - *Return characters with names that begin with the specified string (e.g. Sp).*
* Content-Type: **application/json**

### Authentication

You will need to provide 3 query parameters to authenticate the client.
* **ts**: actual timestamp in milliseconds
* **apikey**: the client's public API key
* **hash**: a generated hash code

We have prepared a tool for you, which you can use to extract these parameters.

    import com.cedevhub.apikey.ApiKeyUtil
    
    val params: Map<String, String> = ApiKeyUtil.getParams(System.currentTimeMillis())

The output of ```ApiKeyUtil.getParams(ts: Long)``` is a ```Map<String, String>```, with the following example content:

    {
	    "ts": "123456789",
	    "apikey": "my-public-api-key",
	    "hash": "generated-hash-key"
	}

Example /characters API call:
https://gateway.marvel.com/v1/public/characters?nameStartsWith=Spide&ts=123456789&apikey=my-public-api-key&hash=generated-hash-key
