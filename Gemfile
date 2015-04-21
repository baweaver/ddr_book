source "https://rubygems.org"

gem 'bundler'
gem 'asciidoctor'
gem 'rake'


group :pdf do
  gem 'asciidoctor-pdf', '~> 1.5.0.alpha.5'
  gem 'coderay'
end

group :epub do
  gem 'asciidoctor-epub3', '~> 1.0.0.alpha.3'
  gem 'kindlegen'
  gem 'epubcheck'
end

group :pdf, :epub do
  gem 'pygments.rb'
end
