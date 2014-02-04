# WP Deploy

**This is not useable yet.**

## A Problem

Deploying WordPress sucks. A common hosting environment looks like this: A shared host that only allows plain FTP access, and has a MySQL server that only accepts localhost connections. Now imagine a modern development workflow:

1. Multiple developers work on their own local copies of the site.
2. They push changes to their personal repositories, and to a shared repository. Tests run automatically.
3. The shared development repo is automatically built and deployed to a main staging site, as long as tests are passing. Tagged releases are deployed to subdomains (tag == subdomain). Clients look at stable staging environment. Tags are used for versioning, and also for feature demos.
4. The main staging site can be deployed to the production site with a single command.

A lot of cheap hosts only allow [S]FTP, and only plain FTP actually works. Nice hosts allow SSH access. Awesome hosts support git based deployment.

- Developers will choose the best protocol for their situation.
- Projects include more than the site itself. The site should be in a subdirectory.

To developers, there should be no distinction between site content, like uploads and database entries, and code. Dummy content is handled like dummy code: it stays out of the master branch, and it is discouraged altogether in favor of tests.

Tests should run both with and without production site content. If a test passes in isolation but not with production site content, then it is likely that there has been a name clash of some sort.

## A Solution

This is gonna hurt, but soon the pain will end.

### Transport Protocol

The deployment system should support transport plugins for [S]FTP, SSH and git. Destinations should be configurable.

### Content

Content is formatted depending on the code. They are coupled. Content must be kept in version control, so that it remains compatible with any commit. This includes uploaded files and databases.

`git pull` should pull in the database content from a remote, and `git push` should merge the local database content to the remote. This could be done by git, working with SQL dumps, or by MySQL using an upsert process.

### Code

Pull, push, ftp from remote to host.

## Preparation

- Learn about WP Roots.
- Learn how to MySQL upsert.
- Grunt git, ftp.
