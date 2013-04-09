### Notes from RailsGuides: Asset Pipeline


- Web browsers are limited in the number of requests that they can make in _parallel_. So fewer requests can mean faster loading of your application

- There are 3 features of the asset pipeline:
    - Concatenate assets: This reducess the number of requests that a browser must make to render a page and hence speeds up the load time
    - Asset Minification or compression
    - Precompiling higher-level language assets: Allows assets to be written in a higher-level language with precompilation down to the actual asset. Supported languages are SASS, Coffeescript, ERB. 

- Pipeline assets can be placed in one of the following locations: 
    - app/assets: owned by the app
    - lib/assets: shared across apps
    - vendor/assets: owned by outside entities

- You can view search path for assets by inspecting `Rails.application.config.assets.path`

- Manifest is used to include/require other assets

