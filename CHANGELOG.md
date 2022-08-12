# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

- Separation of docker-compose into development environments (local/stage/prod).
- Add local ssl and documentation
- Add gitlab CI/CD

## [0.0.3] - 2022-08-12

### Added

- Containers:
    - rabbitmq management 3.10.7 alpine
    - redis 7.0 alpine

### Changed

- CHANGELOG.md
- README.md
- .env.sample
- docker-compose

### Removed

- ...

### Fixed

- ...

## [0.0.2] - 2022-08-05

### Added

- Containers:
    - node js 18 alpine
    - mysql 8
    - nginx 1.23 alpine
    - redis 7.0 alpine
    - mailcatcher

### Changed

- CHANGELOG.md
- README.md
- .env.sample
- Api dockerfile
- docker-compose

### Removed

- ...

### Fixed

- ...

## [0.0.1] - 2022-06-16

### Added

- Containers:
    - php-fpm 8 alpine

- Add base parameters in .env.sample.
- Add LICENSE (MIT License), CHANGELOG.md, README.md.

### Changed

- ...

### Removed

- ...

### Fixed

- ...