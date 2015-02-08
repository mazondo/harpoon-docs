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
      include Harpoon::Service

      # Harpoon::Service lets you define required authorizations
      # once defined, users will be asked for them on first run
      # you'll have access to the auth using @auth[:secret]
      auth :secret, "Access Token"

      # Harpoon::Service lets you define options for your provider
      # once defined, users will be asked for them on first run
      # you'll have access to the options using @options.option_name
      # Harpoon will enforce required options for you, and even verify
      # them as part of `harpoon doctor`
      option :option_name, default: "default value", required: true
      option :option_two_name, required: false

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

## Working with Files
Because your services will be working with files quite a bit, we've made it easy to do.  We'll provide an array of files that need to be deployed (already taking into consideration nested folders configured by users).  To interact with the files, just use the `options` object.

```ruby

def deploy
  @options.files.each do |f|
    #do something with the file
  end
end
```

## Communicating with Users
To communicate with your users, we pass in a logger object.  You can utilize this to send any info to the console.  We'll take care of handling the logging level from the command line.

```ruby

def doctor
  @logger.debug "debug message"
  @logger.info "Info message"
  @logger.warn "warning message"
  @logger.error "Error message"
  @logger.fatal "Fatal message"
  @logger.pass "Pass message"
  @logger.fail "Fail message"
  @logger.suggest "Suggest message"
end
```
