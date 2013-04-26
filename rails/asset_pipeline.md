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

- In production, Rails precompiles these files to public/assets by default. The precompiled copies are then served as static assets by the web server. The files in app/assets are never served directly in production.

- You can view search path for assets by inspecting `Rails.application.config.assets.path`. Default subdirectories that will be searched are images, javascripts and stylesheets. so may be we need to add fonts  and software ? 

- Manifest is used to include/require other assets

- In production, Rails inserts an MD5 fingerprint into each filename so that the file is cached by the web browser. You can invalidate the cache by altering this fingerprint, which happens automatically whenever you change the file contents.

- Fingerprinting is a technique that makes the name of a file dependent on the contents of the file. When the file contents change, the filename is also changed.For content that is static or infrequently changed, this provides an easy way to tell whether two versions of a file are identical, even across different servers or deployment dates.

- Files you want to reference outside a manifest must be added to the precompile array or they will not be available in the production environment.


Source: http://guides.rubyonrails.org/asset_pipeline.html 

