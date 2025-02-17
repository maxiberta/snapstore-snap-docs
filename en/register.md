---
title: Registration
table_of_contents: true
---

# Registration

## Configure private and public keys

You will need to configure an RSA key pair in order to register
the proxy. This acts as the proxy's identity with the upstream Snap Store.

They can be generated and configured automatically:

    sudo snap-proxy generate-keys

Or you can manually generate a key pair, in OpenSSH format (e.g., via
ssh-keygen) and configure it explicitly:

    sudo snap-proxy config \
        proxy.key.public="<public key data>" \
        proxy.key.private="<private key data>"

This key is your proxy's identity and should be
recorded securely. To view keys generated by the `generate-keys` command,
you can run:

    sudo snap-proxy config proxy.key.public proxy.key.private

## Initial registration

To register the proxy, you will need to provide Ubuntu SSO credentials
for the desired account you wish to link the proxy with, and answer
some simple questions about your deployment:

    sudo snap-proxy register --https

or:

    sudo snap-proxy register

If the `--https` option is omitted, the resulting [assertion](devices.md)
instructing client devices to use the proxy instead of the upstream store, will
instruct them to use HTTP to connect to the proxy instead of HTTPS.

You can examine your proxy's registration status with:

    snap-proxy status

This will show the registration status of your proxy, as well as local
status information of this server.

!!! Positive "":
    For evaluation purposes, we automatically grant the use of up to 5 devices.

At this point, your proxy will be assigned a Store ID, which can be retrieved
with the status command. This will be used in later commands and to
identify your proxy for support purposes.

## Next step

Configure the proxy to [serve HTTPS](https.md) traffic if `--https` registration
option was used, or proceed to [configure client devices](devices.md).
