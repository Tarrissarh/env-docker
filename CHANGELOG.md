# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]
- Separation of docker-compose into development environments (local/stage/prod).
- Add local ssl and documentation
- Add gitlab CI/CD

## [0.0.2] - 2022-08-05
### Added
- The basis of the local development environment has been created:
  - node js 18 alpine
  - mysql 8
  - nginx 1.23 alpine
  - redis 7.0 alpine
  - mailcatcher

### Changed
- CHANGELOG.md
- README.md
- .env.sample
- Modify dockerfile api (changed how extensions are installed)

### Removed
- postgres
- node

### Fixed
- ...

## [0.0.1] - 2022-06-16
### Added
- The basis of the local development environment has been created:
  - php-fpm 8 alpine

- Add base parameters .env.sample.
- Add LICENSE (MIT License).
- CHANGELOG.md, README.md.

### Changed
- ...

### Removed
- ...

### Fixed
- ...