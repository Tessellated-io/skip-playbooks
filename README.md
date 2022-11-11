# Skip Playbooks

[Skip](https://skip.money) is an ecosystem aligned MEV solution for Tendermint.  This repository contains a number of playbooks that can be used to apply Skip's software to an existing Tendermint node!

Playbooks here are meant to be compatible with the excellent set of [Tendermint Playbooks provided by Polkachu](https://github.com/polkachu/cosmos-validators), and should work out of the box. 

These playbooks will enter the remote machine, clone the node software, patch Skip into the codebase, restart the daemon and then cleanup after itself. Almost everything is set up to work right out of the box. 

The only assumption this playbook makes is that Tendermint node is run as a `systemd` daemon.

## Getting Started

1. Get an API Key from Skip [here](https://skip.money/registration)
2. Setup `inventory.ini`

To start, copy `inventory.sample.ini` to `inventory.ini`, and customize the IP addresses for the networks you wish to deploy on. Modify any config settings to suit the specifics of how SSH access to the remote machine is configured.

3. Modify Variables

In the `.yml` file corresponding to the network you wish to join (ex. `juno.yml`) there are two variables you may need to change:
  - `daemon` - Leave this as is if you do not use Cosmosvisor, or change to `cosmosvisor` if you do.
  - `relayer_personal_peer_id` - Set this up if the node you are installing on is a sentry node, according to [Skip's documentation](https://www.notion.so/skip-protocol/mev-tendermint-8-b5f300d29c15466e863cd849121d6beb)

Additionally, you may want to glance over the other variables. For most systems, including one's deployed with Polkachu's playbooks,
the default values should be up to date. If you happen to not anything out place (ex. wrong node or Skip version), feel free to send a PR! 

4. Deploy

You can deploy by running the playbook for the target network and specifying your API key: 
```shell
$ ansible-playbook juno.yml --extra-vars skip_api_key=<your API key>
```

This will install Skip on every host in `inventory.ini` that starts with the network name (ex. `juno.yml` would run on `juno-sentry-1`, `juno-sentry-2` and `juno-validator`).

## Tessellated
[<img src="media/logo.png" width="100px" align="left" />](https://tessellated.io)

[Tessellated](https://tessellated.io) contributes to projects across the proof of stake landscape. 

If you find this project helpful, consider [delegating
to us in the future](https://www.mintscan.io/juno/account/juno12udz3pg72mr3yupsguf29nj3gfqlluwqsg4850)! 
