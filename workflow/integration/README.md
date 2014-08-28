# Workflow / Integration

## LiveReload

**Gemfile**

```ruby
...

group :development, :test do
  gem 'rb-fsevent', require: false if RUBY_PLATFORM =~ /darwin/i
  # gem 'terminal-notifier-guard'
  gem 'rack-livereload'
  gem 'guard-livereload', require: false
end

...
```

**Guardfile**

```ruby
guard 'livereload' do
  # watch(%r{app/admin/.+\.(rb)$})
  watch(%r{app/views/.+\.(erb|haml|slim)$})
  watch(%r{app/helpers/.+\.rb})
  watch(%r{public/.+\.(css|js|html)})
  watch(%r{config/locales/.+\.yml})

  # Rails Assets Pipeline
  watch(%r{(app|vendor)(/assets/\w+/(.+\.(css|js|html))).*})# { |m| "/assets/#{m[3]}" }
  
  notification :terminal_notifier
end
```

**CLI**

```bash
$ guard -P livereload
```
