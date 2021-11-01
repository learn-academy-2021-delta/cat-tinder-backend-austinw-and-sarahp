Rails Intro, Seeds, and Cors

```
$ rails new cat_tinder_backend -d postgresql -T 
$ cd cat_tinder_backend
$ rails db:create
$ bundle add rspec-rails
$ rails g rspec:install

$ git remote add origin https://github.com/...
$ git checkout -b main
$ git add .
$ git commit -m "your message here"
$ git push origin main
```

## Swap to a new branch and start working

```
$ rails generate resource Cat name:string age:integer enjoys:text
$ rails db:migrate
$ rails rspec spec

```
<!-- just to make sure things didn't break -->
  
In db/seeds.rb 
```ruby
cats = [
    {
        name: "Felix",
        age: 2,
        enjoys: "Long naps on the couch, and a warm fire"
    },
    {
        name: "Lola",
        age: 5,
        enjoys: "hairball fetish"
    },
    {
        name: "Toast",
        age: 5,
        enjoys: "warm butter"
    },
    {
        name: "Chesire",
        age: 10,
        enjoys: "useless advice"
    }
]

cats.each do |attributes|
    Cat.create attributes
    p "creating cats #{attributes}"
end
```
```
$ rails db:seed
```
CORS
 in the Application controller
 ```ruby
 skip_before_action :verify_authenticity_token
```
  
In the Gemfile

```ruby
 gem 'rack-cors', :require => 'rack/cors'
```

In config/initilaizers add file name "cors.rb"

add this code to the file 
```ruby
# Avoid CORS issues when API is called from the frontend app.
# Handle Cross-Origin Resource Sharing (CORS) in order to accept cross-origin AJAX requests.

# Read more: https://github.com/cyu/rack-cors

Rails.application.config.middleware.insert_before 0, Rack::Cors do
  allow do
    origins '*'  # <- change this to allow requests from any domain while in development.

    resource '*',
      headers: :any,
      methods: [:get, :post, :put, :patch, :delete, :options, :head]
  end
end
```

Useful commands 
$ rails routes
  
stub: A method stub in software development is a piece of code used to stand in for some other programming functionality.
```ruby
def index

end
```

Endpoints: 
- GET "/index" =>  cat#index  
- POST "/create" => cat#create  
- PATCH "/update" => cat#update  
- DELETE "/destroy" => cat#destroy  

    