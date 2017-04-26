# scrapy-monkeylearn

A [Scrapy][scrapy] middleware to categorize items using [MonkeyLearn][ml].

# Settings

|         Option Name           |                         Value                                   |    Example Value            |
|------------------------------ | --------------------------------------------------------------- | --------------------------- |
|`MONKEYLEARN_BATCH_SIZE`       | The size of the item batches sent to MonkeyLearn. Default=200	  | `200`                       |
|`MONKEYLEARN_MODULE`           | The ID of the monkeylearn module.                               | `'cl_oFKL5wft'`             |
|`MONKEYLEARN_USE_SANDBOX`      | In case of using a classifier, if the sandbox version should be used. Default=False  | `False`                     |
|`MONKEYLEARN_TOKEN`            | The auth token.                                                 | `'TWFuIGlzIGRp...'`         |
|`MONKEYLEARN_FIELD_TO_PROCESS` | A field or list of Item text fields to use for classification.  | `['title', 'description']`  |
|`MONKEYLEARN_FIELD_OUTPUT`     | The field where the MonkeyLearn output will be stored.          | `'categories'`              |

An example value of the `MONKEYLEARN_FIELD_OUTPUT` field after classification
is: `[{'label': 'English', 'probability': 0.321}]`.

# Usage

In your settings.py file, add the previously described settings and add `MonkeylearnMiddleware` to your middlewares **with a low number (such as `1`)**, so that this middleware is the last one to be executed when the data is going from the spider to Scrapy engine, e.g.:

```python
SPIDER_MIDDLEWARES = {
    # the MonkeyLearnMiddleware requires a very low order number
    'scrapy_monkeylearn.middlewares.MonkeylearnMiddleware': 1,
}
```

# License

Copyright (c) 2015 [MonkeyLearn][ml].

Released under the MIT license.

[scrapy]: http://scrapy.org/
[ml]: http://www.monkeylearn.com/
