# Bazel Query CLI Helper

This is a small tool, `bqcli`, which adds conveniences to using [`bazel query`](https://docs.bazel.build/versions/master/query.html) from the command line. The first feature is it adds a pipe `|` operator to allow building up queries left to right.

For example, this query determines all tests belonging to any iOS app that depends on the `Modules/BusinessTime` module.

```python
tests(siblings(deps(kind(ios_application, rdeps('Modules/...', 'Modules/BusinessTime')))))
```

Here's the equivalent query written using a `|` operator:

```python
rdeps('Modules/...', 'Modules/BusinessTime') | kind(ios_application) | deps() | siblings() | tests()
```

### Limitations

Bazel query expressions are parsed as Python. Bazel query syntax is not a subset of Python, so it's possible to write queries that `bqcli` does not handle.

### Version

0.0000000000000000001
