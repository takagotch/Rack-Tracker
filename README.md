### Rack::Tracker
---
https://github.com/railslove/rack-tracker



```
gem 'rack-tracker'
bundle
gem install rack-tracker

```

```ruby
config.middleware.use(Rack::Tracker) do
  handler :google_analytics, { tracker: 'U-XXXXX-Y' }
end

web = Rack::Builder.new do
  use Rack::Tracker do
    handler :google_analytics, { tracker: 'U-XXXXX-Y' }
  end
  run Sinatra::Web
end
run web

request.env['tracker'] = {
  'google_analytics' => [
    { 'class_name' => 'Send', 'category' => 'Users', 'action' => 'Login', 'label' => 'Standard' }
  ]
}

config.middleware.use(Rack::Tracker) do
  handler :google_global, { trackers: [ { id: 'U-XXXXX-Y' }, { id: 'U-WWWWW-Z'} ] }
end

def show
  tracker do |t|
    t.google_analytics :send, { type: 'event', category: 'button', action: 'click', label: 'nav-buttons', value: 'X' }
  end
end

ga('send', { 'hitType': 'event', 'eventCategory': 'button', 'eventAction': 'click', 'eventLabel': 'nav-buttons', 'value': 'X' })

def show
  tracker do |t|
    t.google_analytics :parameter, { dimension1: 'pink' }
  end
end

ga('set', 'dimension1', 'pink');

def show
  tracker do |t|
    t.google_analytics :enhanced_ecommerce, {
      type: 'addItem',
      id: '1234',
      name: 'Fluffy Pink Bunnies',
      sku: 'DD23444',
      category: 'Party Toys',
      price: '11.99',
      quantity: '1'
    }
  end
end

ga("", {})

def show
  tracker do |t|
    t.google_analytics :ecommerce, { type: '', id: '', affiliation: '' }
  end
end

config.middleware.use(Rack::Tracker) do
  handler :google_analytics, { tracker: 'U-XXXXX-Y', ecommerce: true }
end

config.middleware.use(Rack::Tracker) do
  handler :google_adwords_conversion, { id: 123456,
                                        language: "en",
                                        format: "3",
                                        color: "ffffff",
                                        label: "Conversion label",
                                        currency: "USD" }
end

def show
  tracker do |t|
    t.google_adwords_conversion :conversion, { value: 10.0 }
  end
end

def show
  tracker do |t|
    t.google_adwords_conversion :conversion, { id: 123456,
                                               language: 'en',
                                               format: '3',
                                               color: 'ffffff',
                                               label: 'Conversion Label',
                                               value: 10.0 }
  end
end


config.middleware.use(Rack::Tracker) do
  handler :google_tag_manager, { container: 'GTM-XXXXXX' }
end

config.middleware.use(Rack::Tracker) do
  handler :google_tag_manager, { container: 'GTM-XXXXXX', turbolinks: true }
end

def show
  tracker do |t|
    t.google_tag_manager :push, { price: 'X', another_variable: ['array', 'values'] }
  end
end

config.middleware.use(Rack::Tracker) do
  handler :facebook_pixel, { id: 'PIXEL_ID' }
end

conifg.middleware.use(Rack::Tracker) do
  handler :facebook_pixel, { id: lambda { |env| env['PIXEL_ID'] } }
end

class MyController < ApplicationController
  def show
    t.facebook_pixel :track, { type: 'Purchase', options: { value: 100, currency: 'USD' } }
  end
end

fbq("track", "Purchase", {"value":"100.0","currency":"USD"});

tracker do |t|
  t.facebook_pixel :track_custom, { type: 'FrequentShopper', options: { purchases: 24, category: 'Sport' } }
end

use Rack::Tracker do
  handler :vmo, { account_id: 'YOUR_ACCOUNT_ID' }
end

config.middleware.use(Rack::Tracker) do
  handler :go_squared, { tracker: 'ABCDEFGH' }
end

_gs('ABCDEFGH');

config.middleware.use(Rack::Tracker) do
  handler :go_squared, {
    trackers: {
      primaryTracker: 'ABCDEFGH',
      secondaryTracker: '1234456',
    }
  }
end

_gs();
_gs();

def show
end

_gs();

def show
end

_gs();

config.middleware.use() do
end

def show
end

window.criteo_q.push();

t.criteo :track_transaction, {}

config.middleware.use() do
end

def show
end

window._zx.push();

zx_category = '';
zx_amount = '';

def show
end

def show
end

config.middleware.use() do
end

class MyHandler < Rack::Tracker::Handler
end

def render
end

config.middleware.use() do
end

class MyHandler < Rack::Tracker::Handler
end

def self.track()
end

```

```
<scirpt>
  console.log('my tracker: ' + <%= options.to_json %>);
</script>

```

