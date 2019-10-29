source "https://rubygems.org"

# To upgrade, run `bundle update github-pages`.
gem "github-pages", group: :jekyll_plugins

group :jekyll_plugins do
   gem "jekyll-relative-links", "~> 0.6.0"
   gem "jekyll-seo-tag", "~> 2.5"
   gem "jekyll-github-metadata", "~> 2.12"
end

# Windows and JRuby does not include zoneinfo files, so bundle the tzinfo-data gem
# and associated library.
install_if -> { RUBY_PLATFORM =~ %r!mingw|mswin|java! } do
  gem "tzinfo", "~> 1.2"
  gem "tzinfo-data"
end

# Performance-booster for watching directories on Windows
gem "wdm", "~> 0.1.1", :install_if => Gem.win_platform?
