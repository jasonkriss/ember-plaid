# ember-plaid

[Plaid's](https://plaid.com/) drop-in Link module as an Ember component.

## Installation

```bash
# From within your ember-cli project
ember install ember-plaid
```

## Configuration

```javascript
// config/environment.js
ENV['ember-plaid'] = {
  clientName: 'REQUIRED',
  product: 'auth',
  key: 'test_key',
  env: 'tartan'
};
```

Check the [Link Docs](https://github.com/plaid/link#custom-integration) for all of the parameter options.

The script tag adding Plaid JS will be automatically added to the body of the
HTML. To disable this option, you can add `scriptTag: false` to `ember-plaid`.

## Usage

```hbs
{{plaid-link action='processPlaidToken'}}

{{!-- Or --}}

{{#plaid-link action='processPlaidToken'}}Verify Bank Account{{/plaid-link}}
```

Once a user has successfully onboarded via Plaid Link, the provided action will be called with the `public_token` passed as the sole argument. From there, you should follow the [instructions](https://github.com/plaid/link#step-3-write-server-side-handler) for exchanging the `public_token` for an `access_token`.

Once you have the `public_token`, you can use it to initialize plaid-link component in "update mode". Update mode allows the user to update Plaid when they change their online-banking credentials or MFA.

```hbs
{{plaid-link
  action='processPlaidToken'
  token=$public_token}}

{{!-- Or --}}

{{#plaid-link
  action='processPlaidToken'
  token=$public_token}}Verify Bank Account{{/plaid-link}}
```

