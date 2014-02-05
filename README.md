# OpenShift Sidekiq Cartridge

**Sidekiq** is a full-featured background processing framework for **Ruby**. It aims to
be simple to integrate with any modern Rails application and much higher
performance than other existing solutions. For more information about Sidekiq
visit the [Sidekiq homepage](http://sidekiq.org/)

This cartridge will allow you to run Sidekiq in your OpenShift Ruby application
whether it is Rails or other Rack compatible app.

This cartridge also provide Sidekiq [monitoring web interface](https://github.com/mperham/sidekiq/wiki/Monitoring)

![monitoring][https://raw2.github.com/mfojtik/openshift-origin-cartridge-sidekiq/master/doc/sidekiq.png]

## Installation

1. [Create your OpenShift account](https://openshift.redhat.com/app/account/new)
2. Create `ruby-1.9` application: `rhc app create myapp ruby-1.9`
3. Add **Redis** cartridge to your application:

```
rhc add-cartridge http://cartreflect-claytondev.rhcloud.com/reflect?github=smarterclayton/openshift-redis-cart --app myapp
```

4. Finally, add **Sidekiq** cartridge to your application:

```
rhc add-cartridge https://raw2.github.com/mfojtik/openshift-origin-cartridge-sidekiq/0.0.3/metadata/manifest.yml --app myapp
```

Now, everything should be properly configured and you should be able to add your
workers. There are two ways you can do this:

### Using Rails

In case you use Ruby on Rails framework, all you need to do is to place your
workers into `app/workers/` directory inside your application repository.

### Using Sinatra/Padrino/Rack

If you are not using Rails, then you need to create `workers.rb` file in your
application repository root and require the workers manually there:

```ruby
# workers.rb
require_relative './lib/sample_worker'
```

### Using monitoring interface

You can access the monitoring interface at `https://YOUR_APP-NAMESPACE.rhcloud.com/sidekiq`.
Sidekiq will print the full URL with authentication after successfull install.
