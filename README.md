# Neighbor Articles: A Plugin for Pelican

[![Build Status](https://img.shields.io/github/workflow/status/pelican-plugins/neighbors/build)](https://github.com/pelican-plugins/neighbors/actions) [![PyPI Version](https://img.shields.io/pypi/v/pelican-neighbors)](https://pypi.org/project/pelican-neighbors/)

Neighbors is a Pelican plugin that adds Next/Previous links to articles.


## Installation

This plugin can be installed via:

    python -m pip install pelican-neighbors


## Usage

This plugin adds a couple of new variables to the article's context:

* `next_article` (newer)
* `prev_article` (older)
* `next_article_in_category`
* `prev_article_in_category`
* `next_article_in_subcategory#`
* `prev_article_in_subcategory#`

Here is an example on how to add article navigation in your Jinja `article.html`
template:

```html+jinja
<ul>
    {% if article.prev_article %}
        <li>
            <a href="{{ SITEURL }}/{{ article.prev_article.url}}">
                {{ article.prev_article.title }}
            </a>
        </li>
    {% endif %}
    {% if article.next_article %}
        <li>
            <a href="{{ SITEURL }}/{{ article.next_article.url}}">
                {{ article.next_article.title }}
            </a>
        </li>
    {% endif %}
</ul>
<ul>
    {% if article.prev_article_in_category %}
        <li>
            <a href="{{ SITEURL }}/{{ article.prev_article_in_category.url}}">
                {{ article.prev_article_in_category.title }}
            </a>
        </li>
    {% endif %}
    {% if article.next_article_in_category %}
        <li>
            <a href="{{ SITEURL }}/{{ article.next_article_in_category.url}}">
                {{ article.next_article_in_category.title }}
            </a>
        </li>
    {% endif %}
</ul>
```

## More Categories plugin support

You can use the `Neighbors` plugin with the [More
Categories](https://github.com/pelican-plugins/more-categories) plugin.

Since an article can belong to more than one subcategory, subcategories are
stored in a list. If you have an article with subcategories like
`foo/bar/baz`, it will belong to both subcategory `bar`, and `bar/baz`.

Subcategory neighbors are added to an article as `next_article_in_subcategory#`
and `prev_article_in_subcategory#` where `#` is the level of subcategory.

Using the example above:
- `sebcategory0` is `foo`
- `subcategory1` will be `foo/bar`
- `subcategory2` will be `foo/bar/baz`

## Subcategory plugin support

You can use the Neighbors plugin in conjunction with the [Subcategory
plugin](https://github.com/getpelican/pelican-plugins/tree/master/subcategory).

Since an article can belong to more than one subcategory, subcategories are
stored in a list. If you have an article with subcategories like
`Category/Foo/Bar`, it will belong to both subcategory `Foo`, and `Foo/Bar`.

Subcategory neighbors are added to an article as `next_article_in_subcategory#`
and `prev_article_in_subcategory#` where `#` is the level of subcategory. So
using the example from above, `subcategory1` will be `Foo`, and `subcategory2`
will be `Foo/Bar`.

## Template Examples

The usage with subcategories from either the Subcategory plugin or the More Categories plugin is:

```html+jinja
<ul>
    {% if article.prev_article_in_subcategory1 %}
        <li>
            <a href="{{ SITEURL }}/{{ article.prev_article_in_subcategory1.url}}">
                {{ article.prev_article_in_subcategory1.title }}
            </a>
        </li>
    {% endif %}
    {% if article.next_article_in_subcategory1 %}
        <li>
            <a href="{{ SITEURL }}/{{ article.next_article_in_subcategory1.url}}">
                {{ article.next_article_in_subcategory1.title }}
            </a>
        </li>
    {% endif %}
</ul>
<ul>
    {% if article.prev_article_in_subcategory2 %}
        <li>
            <a href="{{ SITEURL }}/{{ article.prev_article_in_subcategory2.url}}">
                {{ article.prev_article_in_subcategory2.title }}
            </a>
        </li>
    {% endif %}
    {% if article.next_article_in_subcategory2 %}
        <li>
            <a href="{{ SITEURL }}/{{ article.next_article_in_subcategory2.url}}">
                {{ article.next_article_in_subcategory2.title }}
            </a>
        </li>
    {% endif %}
</ul>
```

## Limitations

If an article has multiple categories, only the first category is considered.


## Contributing

Contributions are welcome and much appreciated. Every little bit helps. You can contribute by improving the documentation, adding missing features, and fixing bugs. You can also help out by reviewing and commenting on [existing issues][].

To start contributing to this plugin, review the [Contributing to Pelican][] documentation, beginning with the **Contributing Code** section.

[existing issues]: https://github.com/pelican-plugins/neighbors/issues
[Contributing to Pelican]: https://docs.getpelican.com/en/latest/contribute.html
