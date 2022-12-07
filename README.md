# Destructive Changes

Use this repo to make destructive changes in an environment. This can be particularly useful for:
 - Apex Classes or Triggers in a production environment where you aren't permitted to delete these items from the UI.
 - Any time you want to automate a delete operation across multiple environments. 

## Prerequisites

- You need to have the sfdx cli installed on your machine.
- You have already authenticated with the environment where you want to delete metadata and have an alias for it. 

## Steps

1. Clone this repo.
2. Edit the destructiveChanges.xml file to specify the metadata you want to delete.
3. From a command prompt, while in the folder with these files, run the command below.

>sfdx force:mdapi:deploy -u environmentAlias --deploydir . --wait 2 --testlevel RunSpecifiedTests  --runtests SListTest

### More info about this command

- You will need to replace 'environmentAlias' with the alias that you specified when you authorized the environment (more info below).
- If you don't specify `--wait 2` the command will return immediately, and you will have to run another SFDX command to see if the job completed successfully. 
- `--testlevel` was specified because Salesforce requires this when you delete Apex classes, even though the test is irrelevant. `SlistTest` was chosen as the test class, simply because it is small and executes quickly. Any other test class can be specified.
- Documentation for the `mdapi:deploy` command can be [found here](https://developer.salesforce.com/docs/atlas.en-us.sfdx_cli_reference.meta/sfdx_cli_reference/cli_reference_force_mdapi.htm#cli_reference_force_mdapi_deploy).

### Authorizing an environment

- The easiest way to authorize an environment is to go into VS Code and select `SFDX: Authorize an Org` which will walk you through the process. 
- You can also do this directly from the SFDX CLI. It is documented [here](https://developer.salesforce.com/docs/atlas.en-us.sfdx_cli_reference.meta/sfdx_cli_reference/cli_reference_auth_web.htm#cli_reference_auth_web_login).
- Whichever way you authorize an environment, you will need to specify an alias, and that alias will be used in the `mdapi:deploy` command above.

## Other Metadata types

- You are not limited to specifying Apex Classes and Triggers as the metadata types in the destructiveChanges.xml file. If you want to specify other types, you will need to know what the 'name' should be. That info can be [found here](https://developer.salesforce.com/docs/atlas.en-us.api_meta.meta/api_meta/meta_types_list.htm).
- Additional info about destructive changes can be [found here](https://developer.salesforce.com/docs/atlas.en-us.daas.meta/daas/daas_destructive_changes.htm).