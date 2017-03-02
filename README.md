# Express OpenID Connect Secured Jekyll

An Express application for securing a Jekyll powered website using OpenID Connect `authorization_flow`, with optional support for JavaScript clients using `client_credentials`.

**Note:** This library is currently targeting IdentityServer3.

## Environment requirements

- Node.js (v6 or v7 is set in **package.json** `engines`)
- Ruby v2
- `gem install bundler`

## Usage quickstart

```
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/ritterim/express-openid-connect-secured-jekyll/master/install.rb)"
```

## Manual usage

- Copy **package.json**, **npm-shrinkwrap.json**, and **server.js** from this repository into the Jekyll site.
- Create **.env** in the Jekyll site using **.env.example** as a template.
- Add the following `exclude` items in the Jekyll site **_config.yml**:
  - **node_modules/**
  - **package.json**
  - **npm-shrinkwrap.json**
  - **server.js**
- Add **node_modules/** to **.gitignore** if the target is a Git repository and it does not already contain this entry.
- Deploy the Jekyll blog as a Node.js application.

## Configuration

- HTTPS is required for the `express-session` generated cookie, unless the `EXPRESS_INSECURE` environment variable is set to `"true"`.
- If `'trust proxy'` should be set for Express based on the hosting environment, set `TRUST_PROXY` environment variable to `"true"`.
- To access the cookie generated by `express-session` from JavaScript, set the `SESSION_COOKIE_ALLOW_JS_ACCESS` environment variable to `"true"`.
- To enable bearer token authentication, set the `TOKEN_VALIDATION_URL` environment variable.
  - A `POST` will be performed using `application/x-www-form-urlencoded` with the request body of `token=the_token_value`.

## JavaScript usage

For scenarios when JavaScript on the page needs to make authenticated calls:

- Set the `SET_BEARER_TOKEN_COOKIE_FOR_JAVASCRIPT` environment variable to true
- Set the `CLIENT_CREDENTIALS_SCOPE` environment variable to your scope(s).

`grant_type: client_credentials` will be used for requesting a token. A cookie will be used with a default name of `token`. The cookie name can be overridden using the `process.env.BEARER_TOKEN_COOKIE_NAME` environment variable.

## Public URLs

Set the `PUBLIC_URLS` environment variable using a comma or semicolon delimited string.

- Specifying `/assets` will everything under that path.
- Matches are case insensitive.
- **NOTE: Specifying a url of `/` will make the entire site public.**

**Example:**

```
/assets, /2017/01/01/a-test-post.html
```

## Development quickstart

- `cp .env.example .env`
- Add configuration in **.env**
- `npm install`
- `npm start`

If you encounter issues running locally with SSL certification validation, try adding `NODE_TLS_REJECT_UNAUTHORIZED=0` to **.env**. This should only be done in a local development scenario. See https://stackoverflow.com/a/21961005 answering https://stackoverflow.com/questions/10888610/ignore-invalid-self-signed-ssl-certificate-in-node-js-with-https-request.

## Development choices rationale

This repository is designed being able to easily copy a small number of files into a Jekyll site to add authentication.

## Author

Ritter Insurance Marketing https://www.ritterim.com

## License

- **MIT** : http://opensource.org/licenses/MIT
