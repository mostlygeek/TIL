# Using `versioncmp` in a conditional

Sometimes applications change the name of a script that should run. To have puppet be backwards and forwards compatible use [versioncmp](https://docs.puppetlabs.com/puppet/latest/reference/function.html#versioncmp). 

`versioncmp` will return:

* `1` - if version is greater than
* `0` - if version is equal
* `-1` - if version is less than

```
if versioncmp($app_version, '2.0.1') < 0 {
  $script_name = 'oldscript.sh'
} else {
  $script_name = 'newscript.sh'
}

exec { 'mything': 
  command => "${script_name} woot"
  ...
}

```