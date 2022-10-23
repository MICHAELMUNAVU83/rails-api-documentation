
## CREATING A NEW API APP 
rails new my_api --api --database=postgresql

## CREATE A NEW MODEL
rails g model Article title:string body:text

## CREATING A NEW MODEL THAT REFERS TO ANOTHER MODEL
rails g model Review title:references rating:integer  article:references

## ADD DATA TO THE DATABASE VIA SEED.RB


airlines = Airline.create([
    { 
        name: "United Airlines",
        image_url: "https://open-flights.s3.amazonaws.com/United-Airlines.png"
    },
    {
        name: "Southwest",
        image_url: "https://open-flights.s3.amazonaws.com/Southwest-Airlines.png"
    }
    ])
reviews = Review.create([
    {
        title: "Great airline",
        description: "I had a lovely time.",
        score: 5,
        airline: airlines.first
    },
    {
        title: "Bad airline",
        description: "I had a bad time.",
        score: 1,
        airline: airlines.first
    }
])

## CREATE CONTROLLERS  WITH API AND NAMESPACES

rails g controller api/v1/airlines
rails g controller api/v1/reviews

## CREATE A ROUTE FOR THE CONTROLLER

namespace :api do
    namespace :v1 do
        resources :airlines, 
        resources :reviews
    end
end



##  ADD THIS LINE ON CONTROLLERS  TO ALLOW CROSS ORIGIN REQUESTS

    protect_from_forgery with: :null_session

## IF YOU WANT TO CONFIGURE CORS FOR A SPECIFIC RESOURCE, YOU CAN DO IT LIKE THIS
Add this to the gem file

gem 'rack-cors'

Run bundle install

then add this to the config/initializers/cors.rb file
Rails.application.config.middleware.insert_before 0, Rack::Cors do
  allow do
    origins 'http://example.com:80'
    resource '*', headers: :any, methods: [:get, :post]
  end
end



    