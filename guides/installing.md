## Containers and VMs
* [Docker](docker)

## Operating System
* CentOS
* Ubuntu
* [Debian](debian)
* FreeBSD
* Windows

Or are you just looking for the [MySQL Installation](mysql) guide?

## Recommended Hosting Providers
* [DigitalOcean](https://m.do.co/c/18e003a00d57 )

	Using our link will give you $200 in free credit to try any of DigitalOcean's services for 60 days.

	DigitalOcean is a great choice for hosting rAthena. It's cheap, easy to use, and has a great community with many help-topics.

* [OVH](https://www.ovhcloud.com/en-gb/vps/)

	OVH is another great choice for hosting rAthena. It's fairly cheap and runs on a robust network.

*No one at rAthena will **ever** recommend a hosting provider that explicitly advertises "RO Hosting" packages. They are garbage and should be avoided at all costs.*

## Optional Clone Information
If you want to have your own forked version but still get updates from the main rAthena repository

  * Fork this repository to your GitHub account
  * List the current configured remote repository for your fork:

        git remote -v

  * Specify a new remote upstream repository that will be synced with your fork:

        git remote add upstream https://github.com/rathena/rathena.git

  * Verify the new upstream repository you've specified for your fork:

        git remote -v

  * You should see the main rAthena repository as well as your forked repository
  * Now, when you want to get updates from rAthena, simply do:

        git pull upstream master

* Remember that rAthena falls under [GNU GPLv3](https://github.com/rathena/rathena/blob/master/LICENSE).
