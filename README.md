# Fitbyte

Fitbyte is a gem that allows interaction with [Fitbit's REST API](https://dev.fitbit.com/docs/basics/), using the OAuth 2.0 protocol for user authorization.

**Please Note:** Fitbit's API is currently in beta, and is in active/rapid development. Early releases of this gem may introduce some breaking changes until Fitbit's API solidifies.

## Installation

To install the latest release:

    $ gem install fitbyte

To include in a Rails project, add it to the Gemfile:

```ruby
gem "fitbyte"
```

## Usage

To use the Fitbit API, you must register your application at [dev.fitbit.com](https://dev.fitbit.com/apps). After registering, you should have a **CLIENT ID**, **CLIENT SECRET**, and **REDIRECT URI** available for use in instantiating a *Fitbyte::Client* object.

- Create a client instance:

```ruby
client = Fitbyte::Client.new(client_id: my_client_id, client_secret: my_client_secret, redirect_uri: "http://example.com")
```

- Generate a link for the Fitbit authorization page:

```ruby
client.auth_page_link
# => https://fitbit.com/oauth2/authorize?client_id=123XYZ&redirect_uri=...
```

- Follow generated link to Fitbit's authorization page. After approving your app, you're sent to the `redirect_uri`, with an appended authorization `code`, which you'll exchange for an access token:

```ruby
client.get_token(auth_code)
```

You are now authenticated and can make calls to Fitbit's API:

```ruby
client.food_logs
# => returns JSON of current day's food logs
```

## License

The gem is available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT).
