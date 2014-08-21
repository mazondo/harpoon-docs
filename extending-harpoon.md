# Extending Harpoon
Extending harpoon is pretty easy.  Just add your own services, and make sure they repond to the following functions:

 * setup - sets everyting up for future deploys
 * deploy - deploys
 * list - lists available rollbacks
 * rollback - rolls back to a specified release
 * doctor - checks that things are setup correctly

An example service might look like this:

```ruby
module Harpoon
	module Services
		class HostingProvider
			attr_accessor :config, :requests

			def initialize(config, auth, logger)
				@auth = auth
				@config = config
				@logger = logger
			end

			def setup
        #setup for future deploys
			end

      def deploy
        #deploy new code
      end

      def list
        #list available rollbacks
      end

      def rollback(version)
        #rollback to {{version}}
      end

      def doctor
        #check to see if we're ready for a deploy
      end
		end
	end
end
```

Once that's ready, users can utilize your service by setting their config `hosting` attribute to:

```json
{
  "hosting" : "hosting_provider"
}
```

## Accessing Auth Keys
Most service providers will require auth keys, so we've made it really easy to request and store auth tokens from users.

When your service is initialized, it'll be passed an auth object.  You can request keys from that object, which will in turn interact with the user to get keys, for example:

```ruby
  def initialize(config, auth, logger)
    @keys = auth.get_or_ask("hosting_provider", "secret key", "public key")
    # The first string is your namespace for storing the auth keys for the future
    # the second and third strings are what we'll ask the user for if we haven't already
    # stored something for them.
  end
```

## Other config options
In addition to the auth object, you're also passed in a config object that gives you access to everything users stored in their config folder.  We suggest hosting specific options be namespaced under `hosting_options`

```ruby
def initialize(config, auth, logger)
  s3_region = config.hosting_options["region"]
end
```

## Working with Files
Because your services will be working with files quite a bit, we've made it easy to do.  We'll provide an array of files that need to be deployed (already taking into consideration nested folders configured by users).  To interact with the files, just use the `config` object.

```ruby
def initialize(config, auth, logger)
  @config = config
end

def deploy
  @config.files.each do |f|
    #do something with the file
  end
end
```

## Communicating with Users
To communicate with your users, we pass in a logger object.  You can utilize this to send any info to the console.  We'll take care of handling the logging level from the command line.

```ruby
def initialize(config, auth, logger)
  @logger = logger
end

def doctor
  @logger.debug "debug message"
  @logger.info "Info message"
  @logger.warn "warning message"
  @logger.error "Error message"
  @logger.fatal "Fatal message"
end
```
