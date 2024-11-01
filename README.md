# Overview
Email validation utilities for ActiveModel with MX/domain verification support.

# Installation
Gemfile:
    gem 'valid_email'

Basic implementation:
    require 'valid_email'
    
    class Person
      include ActiveModel::Validations
      attr_accessor :name, :email
      
      validates :email, :presence => true, :email => true
    end
    
    p = Person.new
    p.email = "john@doe.com"
    p.valid? # => true
    
    p.email = "invalid@format"
    p.valid? # => false

## Advanced Validation Options

MX record verification:
    validates :email, :email => {:mx => true}

MX with A record fallback:
    validates :email, :email => {:mx_with_fallback => true}

Domain format check (regex-based, no external calls):
    validates :email, :email => {:domain => true}

Block disposable email providers:
    validates :email, :email => {:ban_disposable_email => true}

Minimal setup (skip MX dependencies):
    require 'valid_email/email_validator'

## Standalone Usage

For non-model contexts:
```ruby
ValidateEmail.valid?('test@example.com')
ValidateEmail.mx_valid?('test@example.com')
ValidateEmail.mx_valid_with_fallback?('test@example.com')
```

Load standalone:
    gem 'valid_email', require: 'valid_email/validate_email'

## Extensions

Enable String/Nil methods via Gemfile:
```ruby
gem 'valid_email', require: ['valid_email/all_with_extensions']
```

Usage:
```ruby
nil.email? # => false
"user@domain.org".email? # => true (if valid)
```

## CI Status
[![Build Status](https://travis-ci.org/hallelujah/valid_email.svg?branch=master)](https://travis-ci.org/hallelujah/valid_email)

# Contributing
Fork → Branch → Test → PR. Avoid modifying version/history unless necessary.

# License
Copyright &copy; 2011 Ramihajamalala Hery. See LICENSE.

**Maintainers**: hery[at]rails-royce.org, francesco.belladonna[at]gmail.com, dusanek[at]iquest.cz
