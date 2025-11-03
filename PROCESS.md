# Process followed to upload the page
deploy.yml: 
```
service: recipie_book
image: recipie_book
servers:
  web:
    - 138.68.8.185
env:
  secret:
    - RAILS_MASTER_KEY
  clear:
    SOLID_QUEUE_IN_PUMA: true
    RAILS_ENV: production
    RAILS_LOG_TO_STDOUT: "1"
    RAILS_SERVE_STATIC_FILES: "1"
aliases:
  console: app exec --interactive --reuse "bin/rails console"
  shell: app exec --interactive --reuse "bash"
  logs: app logs -f
  dbc: app exec --interactive --reuse "bin/rails dbconsole"
volumes:
  - "recipie_book_storage:/rails/storage"
  - "recipie_book_db:/rails/db"
asset_path: /rails/public/assets
builder:
  arch: amd64
  remote: ssh://root@138.68.8.185
ssh:
  user: root
```

Production.rb
```
config.action_mailer.default_url_options = { host: "138.68.8.185", protocol: "http" }
config.hosts << "138.68.8.185"
```