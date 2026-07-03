# Modified Zabbix Docker

This repository is a fork of the original located here: [Zabbix Docker](https://github.com/zabbix/zabbix-docker)

## Summary
The docker files for the server component have a few additional packages installed to support [UniFi Zabbix](https://github.com/patricegautier/unifiZabbix)

### Changes
The following packages are installed into the "Dockerfiles > server-pgsql" docker files since I only use a pgsql backend.  As I maintain only the Ubuntu and Alpine variants I have removed the rest of the distribution folders:

            openssh-client 
            jq 
            expect

Upstream zabbix docker has moved to a github-actions style build structure where all the templates and scripts are consolidated into a parent folder instead of broken out under each application/distro.  However, the github-actions build structure is coded towards using github native runners.  I have adapted the github workflow actions to run locally via nektos/act.

- images_build_act.yml is the adapted file while the standard images_build.yml is untouched and moved to "workflows_original" directory to avoid running when publishing releases
- cosign uses a locally generated key pair
- attest has been removed from the images_build_act.yml process since it is not compatible with running nektos/act locally 

To run with netkos/act locally invoke a similar command within the project directory.  A secrets file and var file is necessary with the relevant contents

```
act --secret-file ../.secrets --var-file ../.vars -W .github/workflows/images_build_act.yml -s ACTIONS_STEP_DEBUG=true  > ../log.log
```