# Changelog

All notable changes to this project will be documented in this file, in reverse chronological order by release.

## 2.5.3 - TBD

### Added

- Default behavior changed when malformed is pushed into toUtf8.  Rather than dumping the bad string in an exception (dangerous behavior), it will return a blank string.
- Boolean 'debug' parameter added as second constructor argument, that preserves the old behavior when set to true. 

### Deprecated

- Nothing.

### Removed

- Nothing.

### Fixed

- Nothing.

## 2.5.2 - 2016-06-30

### Added

- [#11](https://github.com/zendframework/zend-escaper/pull/11),
  [#12](https://github.com/zendframework/zend-escaper/pull/12), and
  [#13](https://github.com/zendframework/zend-escaper/pull/13) prepare and
  publish documentation to https://zendframework.github.io/zend-escaper/

### Deprecated

- Nothing.

### Removed

- Nothing.

### Fixed

- [#3](https://github.com/zendframework/zend-escaper/pull/3) updates the
  the escaping mechanism to add support for escaping characters outside the Basic
  Multilingual Plane when escaping for JS, CSS, or HTML attributes.
