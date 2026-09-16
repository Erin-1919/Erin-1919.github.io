source "https://rubygems.org"

gem "jekyll", "~> 3.9"

# Ruby 3.4 removed these from stdlib; Jekyll 3.9 will not boot without them.
gem "csv"
gem "base64"
gem "logger"
gem "bigdecimal"

group :jekyll_plugins do
  gem "jekyll-email-protect"
  gem "jekyll-redirect-from"
  gem "jekyll-paginate"
  gem "jekyll-feed"
  gem "jekyll-seo-tag"
end

gem "tzinfo-data", platforms: [:mingw, :mswin, :x64_mingw, :jruby]
gem "wdm", "~> 0.2" if Gem.win_platform?
gem "webrick", "~> 1.7"
gem "kramdown-parser-gfm"
