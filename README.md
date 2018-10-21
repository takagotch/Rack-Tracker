### Rack::Tracker
---
https://github.com/railslove/rack-tracker



```
gem 'rack-tracker'
bundle
gem install rack-tracker

```

```ruby

use Rack::Tracker do
  handler :maybe_a_friendly_tracker, { tracker: 'U-XXXXX-Y', DO_NOT_RESPECT_DNT_HEADER: true }
  handler :google_analytics, { tracker: 'U-XXXXX-Y' }
end


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

ga("ec:addItem", {"id": "1234", "name": "Fluffy Pink Bunnies", "sku": "DD23444", "category": "Party Toys", "price": "11.99", "quantity": "1"});

def show
  tracker do |t|
    t.google_analytics :ecommerce, { type: 'addItem', id: '1234', affiliation: 'Acme Cloting', revenue: '11.99', shipping: '5', tax: '1.29' }
  end
end

ga('ecommerce:addItem', { 'id': '1234', 'affiliation': 'Acme Clothing', 'revenue': '11.99', 'shipping': '5', 'tax': '1.29' })

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

_gs('ABCDEFGH', 'primaryTracker');
_gs('1234567', 'secondaryTracker');

def show
  tracker do |t|
    t.go_squared :visitor_name, { name: 'John Doe' }
  end
end

_gs("set", "visitorName", "John Doe");

def show
  tracker do |t|
    t.go_squared :visitor_info, { age: 35, favorite_food: 'pizza' }
  end
end

_gs("set", "visitor", { "age": 35, "favorite_food": "pizza" });

config.middleware.use(Rack::Tracker) do
  handler :criteo, { set_account: '1234' }
end

def show
  tracker do |t|
    t.criteo :view_item, { item: 'P0001' }
  end
end

window.criteo_q.push({"event": "viewItem", "item": "P001"});

t.criteo :track_transaction, { id: 'id', item: { id: "P0038", price: "6.54", quantity: 1 } }

config.middleware.use(Rack::Tracker) do
  handler :zanox, { account_id: '1234' }
end

def show
  tracker do |t|
    t.zanox :mastertag, { id: "XXXXXXXXXXX", category: 'Swimming', amount: '3.50' }
  end
end

window._zx.push({"id": "XXXXXXXXXXX"});

zx_category = 'Swimming';
zx_amount = '3.50';

def show
  tracker do |t|
    t.zanox :lead, { order_i_d: 'DEFC-4321' }
  end
end

def show
  tracker do |t|
    t.zanox :sale, { customer_i_d: '123456', order_i_d: 'DEFC-4321', currency_symbol: 'EUR', total_price: '150.00' }
  end
end

config.middleware.use(Rack::Tracker) do
  handler :hotjar, { site_id: '1234' }
end

class MyHandler < Rack::Tracker::Handler
end

def render
  Tilt.new( File.join( File.dirname(__FILE__), 'template', 'my_handler.erb') ).render(self)
end

config.middleware.use(Rack::Tracker) do
  handler MyHandler, { awesome: true }
end

class MyHandler < Rack::Tracker::Handler
  self.positoin = :body
end

def self.track(name, *event)
end

```

```
<scirpt>
  console.log('my tracker: ' + <%= options.to_json %>);
</script>

```

