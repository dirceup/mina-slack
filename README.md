# Mina::Slack

[Slack](https://slack.com) web hook from [mina](https://github.com/nadarei/mina).

## Installation

Add this line to your application's Gemfile:

    gem 'mina-slack', require: false

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install mina-slack

mina 0.3.x:

    gem 'mina-slack', '~> 0.3.0', require: false

In your slack settings, create new Incomming WebHooks and get WebHooks URL.

## Usage

### Load the recipe
Include the recipe in your deploy.rb

```ruby
# config/deploy.rb
require 'mina/slack'

task :deploy do
  deploy do
    invoke :'slack:starting'
    ...

    on :launch do
      ...
    end
  end

  run(:local) do
    invoke :'slack:finished'
  end
end
```


### Setup Slack Details
You'll need to setup your Slack details with an API key, room and subdomain. You can add these as ENV variables or in the `config/deploy/environment.rb`

    # required
    set :slack_env_token, "webhook_token" # comes from inbound webhook integration
    set :slack_env_room, "#general" # the room to send the message to
    set :slack_env_subdomain, "example" # if your subdomain is example.slack.com
    set :application_name, "Example"
    
    # optional
    set :slack_env_stage, "staging"

Or use the ENV variables:

    # required
    ENV['SLACK_TOKEN'] = ''
    ENV['SLACK_ROOM'] = ''
    ENV['SLACK_SUBDOMAIN'] = ''
    ENV['SLACK_APPLICATION'] = ''

    # optional
    ENV['SLACK_STAGE'] = ''
    ENV['SLACK_USERNAME'] = ''
    ENV['SLACK_EMOJI'] = ''

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
