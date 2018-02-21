# Changelog

## 2018-02-21: 0.9.2:

  - Add logrotate configuration using `consul_logrotate_config` var, and
    enabled with `consul_logrotate_enabled`

## 2017-08-16: 0.9.1:

  - Toggle to start consul when running the playbook (defaults to true)

## 2017-07-31: 0.9.0:

  - Deprecated `consul_ui`, moved to `consul_ui_legacy` for backward compat.
    Since consul `0.9.0` the ui is shipped as part of the binary. If you run
    a version older than `0.9.0` and want to use this role along with the UI,
    then just update the `consul_ui` var name.
  - Bumped default consul version to `0.9.0`
  - Bumped ansible version used in tests

## 2017-07-31: 0.7.0

   No changes. Just a tag helper to identify legacy settings for the role

## 2017-05-10: 0.1.2

  - Initscript error: The priority in which the script was executed when
    the system is going down was too high, making `consul leave` fail since
    the network was already down

## 2017-03-17: 0.1.1

  - Ansible lint - Fixed task missing name

## 2017-01-12: 0.1.0

  - Initial release

