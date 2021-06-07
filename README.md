[![Creative Commons cc-sa](http://ForTheBadge.com/images/badges/cc-sa.svg)](https://creativecommons.org/licenses/by-sa/4.0) 
[![UTD powered-by-electricity](http://ForTheBadge.com/images/badges/powered-by-electricity.svg)](https://github.com/gigamaster/ui-theme-doc)
[![UTD](https://forthebadge.com/images/badges/built-with-love.svg)](https://github.com/gigamaster/ui-theme-doc)


<br><br>
<p align="center">
    <h1 align="center">UI Theme Doc (Just the Docs)</h1>
    <p align="center">A modern, highly customizable, and responsive Jekyll theme for documentation with built-in search.<br>Easily hosted on GitHub Pages with few dependencies.</p>
    <p align="center"><strong><a href="https://gigamaster.github.io/ui-theme-doc/">See it in action!</a></strong></p>
    <br><br><br>
</p>

![jtd](https://user-images.githubusercontent.com/896475/47384541-89053c80-d6d5-11e8-98dc-dba16e192de9.gif)

## Installation

Add this line to your Jekyll site's Gemfile:

```ruby
gem "ui-theme-doc"
```

And add this line to your Jekyll site's `_config.yml`:

```yaml
theme: ui-theme-doc
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install ui-theme-doc

Alternatively, you can run it inside Docker while developing your site

    $ docker-compose up

## Usage

[View the documentation](https://gigamaster.github.io/ui-theme-doc/) for usage information.

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/gigamaster/ui-theme-doc. This project is intended to be a safe, welcoming space for collaboration, and contributors are expected to adhere to the [Contributor Covenant](http://contributor-covenant.org) code of conduct.

### Submitting code changes:

- Open a [Pull Request](https://github.com/gigamaster/ui-theme-doc/pulls)
- Ensure all CI tests pass
- Await code review
- Bump the version number in `ui-theme-doc.gemspec` and `package.json` according to [semantic versioning](https://semver.org/).

### Design and development principles of this theme:

1. As few dependencies as possible
2. No build script needed
3. First class mobile experience
4. Make the content shine

## Development

To set up your environment to develop this theme, run `bundle install`.

Your theme is set up just like a normal Jekyll site! To test your theme, run `bundle exec jekyll serve` and open your browser at `http://localhost:4000`. This starts a Jekyll server using your theme. Add pages, documents, data, etc. like normal to test your theme's contents. As you make modifications to your theme and to your content, your site will regenerate and you should see the changes in the browser after a refresh, just like normal.

When the theme is released, only the files in `_layouts`, `_includes`, and `_sass` tracked with Git will be released.

## License

The theme is available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT).
