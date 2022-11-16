# Chart: Admission Controller

## Change Log

This file documents all notable changes to the Admission Controller Helm Chart. The release numbering uses [semantic versioning](http://semver.org).

## v0.7.4
### Minor changes
* Added unit tests to check local overrides of global values

## v0.7.2
### Minor changes
* Add proper validation check for Secure API Token

## v0.7.1
### Minor changes
* Fix bug while using secureAPITokenSecret, removed hard requirement for secureAPIToken

## v0.7.0
### Major changes

* Add support for global values, allows admission-controller to be used as dependency of the sysdig-deploy chart
* Add namespace field to all resources

## v0.6.24

### Minor changes

* Added RBAC enable/disable flag