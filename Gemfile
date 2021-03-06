source 'https://rubygems.org'

if Gem::Version.new(Bundler::VERSION) < Gem::Version.new('1.5.0')
  abort "Redmine requires Bundler 1.5.0 or higher (you're using #{Bundler::VERSION}).\nPlease update with 'gem update bundler'."
end

gem "rails", "4.2.8"
gem "addressable", "2.4.0" if RUBY_VERSION < "2.0"
if RUBY_VERSION < "2.1"
  gem "public_suffix", (RUBY_VERSION < "2.0" ? "~> 1.4" : "~> 2.0.5")
end
gem "jquery-rails", "~> 3.1.4"
gem "coderay", "~> 1.1.1"
gem "request_store", "1.0.5"
gem "mime-types", (RUBY_VERSION >= "2.0" ? "~> 3.0" : "~> 2.99")
gem "protected_attributes"
gem "actionpack-xml_parser"
gem "roadie-rails", "~> 1.1.1"
gem "roadie", "~> 3.2.1"
gem "mimemagic"
gem "mail", "~> 2.6.4"

gem "nokogiri", (RUBY_VERSION >= "2.1" ? "~> 1.8.1" : "~> 1.6.8")
gem "i18n", "~> 0.7.0"
gem "ffi", "1.9.14", :platforms => :mingw if RUBY_VERSION < "2.0"

# Request at least rails-html-sanitizer 1.0.3 because of security advisories
gem "rails-html-sanitizer", ">= 1.0.3"

# Windows does not include zoneinfo files, so bundle the tzinfo-data gem
gem 'tzinfo-data', platforms: [:mingw, :x64_mingw, :mswin]
gem "rbpdf", "~> 1.19.5"

# Optional gem for LDAP authentication
group :ldap do
  gem "net-ldap", "~> 0.12.0"
end

# Optional gem for OpenID authentication
group :openid do
  gem "ruby-openid", "~> 2.3.0", :require => "openid"
  gem "rack-openid"
end

platforms :mri, :mingw, :x64_mingw do
  # Optional gem for exporting the gantt to a PNG file, not supported with jruby
  group :rmagick do
    gem "rmagick", ">= 2.14.0"
  end

  # Optional Markdown support, not for JRuby
  group :markdown do
    gem "redcarpet", "~> 3.4.0"
  end
end

# Include database gems for the adapters found in the database
# configuration file
require 'erb'
require 'yaml'

group :development, :test do
  gem 'sqlite3'
end

group :production do
  gem 'pg'
  gem 'rails_12factor'
  gem 'thin' # change this if you want to use other rack web server
end


group :development do
  gem "rdoc", "~> 4.3"
  gem "yard"
end

group :test do
  gem "minitest"
  gem "rails-dom-testing"
  gem "mocha"
  gem "simplecov", "~> 0.9.1", :require => false
  # TODO: remove this after upgrading to Rails 5
  gem "test_after_commit", "~> 0.4.2"
  # For running UI tests
  gem "capybara", '~> 2.13'
  gem "selenium-webdriver", "~> 2.53.4"
end

local_gemfile = File.join(File.dirname(__FILE__), "Gemfile.local")
if File.exists?(local_gemfile)
  eval_gemfile local_gemfile
end

# Load plugins' Gemfiles
Dir.glob File.expand_path("../plugins/*/{Gemfile,PluginGemfile}", __FILE__) do |file|
  eval_gemfile file
end
