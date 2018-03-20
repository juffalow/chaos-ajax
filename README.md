# Chaos AJAX

[![License](https://img.shields.io/badge/License-MIT-blue.svg?maxAge=2592000)](https://github.com/juffalow/chaos-ajax/blob/master/LICENSE)

Chaos Ajax will change the AJAX response from time to time, so your application
cannot rely on getting only successful response from the server. It makes you
think what is going to happen if API is not working or something goes wrong.

This project was inspired by [Chaos Monkey](https://github.com/Netflix/chaosmonkey)

## Installation

```shell
npm install

# or

yarn install
```

## Build

```shell
npm run Build

# or

yarn run build
```

## How it works

Just add the script to the header or to the end of your page and call `chaos();`.

```html
<script src="bundle.js"></script>
<script>
  chaos();
</script>
```

## Options

#### Probability

The default probability that the request returns empty array is 10%. If you
need higher / lower probability, you can change it by calling:

```javascript
// change the probability to 100%

chaosAjax({probability: 1});
```

#### Only specific url(s)

If you need to change the response for a specific url:

```javascript
chaosAjax({
  probability: 0,
  urls: {
    'http://example.com/something': {
      responseText: '',
    }
  }
});
```

This will change the probability to 0%, so it will not change any other request / response.
And set the condition to only one URL which means anytime the front-end will make request on that specific
URL, it will get empty responseText.

#### Change status code

If you need to test, what your application does if it gets `401 Unauthorized`, just change the default response object:

```javascript
chaosAjax({
  defaultResponse: {
    responseText: '{}',
    status: 401,
    statusText: 'Unauthorized',
  }
});
```

Or if you need to test only a specific URL to return `401 Unauthorized`:

```javascript
chaosAjax({
  probability: 0,
  urls: {
    'http://example.com/something': {
      responseText: '',
      status: 401,
      statusText: 'Unauthorized',
    }
  }
});
```

## License

[MIT license](./LICENSE)
