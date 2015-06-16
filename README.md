# nsidc-search-solr

This vagrant project stands up a Solr instance for NSIDC Search / Arctic Data
Explorer.

NOTE: this README is up to date with the master branch, meaning it may contain
information for an unreleased version of **puppet-nsidc-solr**. For details on
what may have changed since the version you are using, see the
[Changelog](https://bitbucket.org/nsidc/puppet-nsidc-solr/src/master/CHANGELOG.md). For
past versions of the README, see the
[source](https://bitbucket.org/nsidc/search-solr/src), open the branch/tag
dropdown, and select the tag for the desired version.

# Requirements

## NSIDC
For use at NSIDC, this project requires the [vagrant-nsidc-plugin](https://bitbucket.org/nsidc/vagrant-nsidc-plugin).

Dependencies are defined in the CI configuration and should be available upon machine provision.

## Non-NSIDC
When using outside of the NSIDC environment, the confgiruation that would normally
be applied via the configuration in puppet/* will not be applied, and solr will
not be setup to run.

To use this project you will have to set up an environment with the following
requirements met:

*  Ruby environment for acceptance testing:
  *  Ruby (>1.9.3) with development headers (ruby-dev/ruby-devel)
  *  [Bundler](http://bundler.io/)
  *  gcc or another compiler
  *  Requirements for nokogiri:
    *  [libxml2/libxml2-dev](http://xmlsoft.org/)
    *  [zlibc](http://www.zlibc.linux.lu/)
    *  [zlib1g/zlib1g-dev](http://zlib.net/)
* [Solr 4.10.3](https://archive.apache.org/dist/lucene/solr/4.10.3/) installed
* All [requirements](https://lucene.apache.org/solr/4_10_3/SYSTEM_REQUIREMENTS.html) for Solr 4.10.3


# Setup

## NSIDC
The virtual machine will be provisioned using the
[puppet-nsidc-solr](https://bitbucket.org/nsidc/puppet-nsidc-solr) module.
NSIDC Search / Arctic Data Explorer configurations will be applied once Solr is
installed.

To provision the machine:
```shell
vagrant nsidc up --env=dev
```

Once provisioning is complete, the Solr dashboard is accessible from
[http://<environment>.search-solr.apps.int.nsidc.org:8983/solr](), where
<environment> is one of dev, integration, qa, etc.

Additionally if the VM is brought up via the CI jenkins job (as defined in ci.yaml)
[ search-solr-tools](https://bitbucket.org/nsidc/search-solr-tools) will be deployed
 and available on the newly-provisioned machine.  

## Non-NSIDC

Solr by default comes with a configured jetty out of the box.   You can run a local
SOLR instance from {}/solr start -e cloud -noprompt (see
   https://lucene.apache.org/solr/quickstart.html).

To configure solr to use NSIDC's schema.xml and other configurations, move the
files in config/* to the location (modified for your environment) listed in the
puppet/site.pp

## Development

Instructions and notes for developing this project are in
[DEVELOPMENT](https://bitbucket.org/nsidc/puppet-nsidc-solr/src/master/DEVELOPMENT.md).
