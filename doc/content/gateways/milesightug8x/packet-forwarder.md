---
title: "Connect Milesight UG8X with UDP Packet Forwarder"
description: ""
---

This section contains instructions for connecting the Milesight UG8X LoRaWAN gateway to {{% tts %}} using the UDP Packet Forwarder.

<!--more-->

In the **Packet Forwarder** menu and **General** tab, click the little **+** button to create a new server.

{{< figure src="../plus.png" alt="Create new server" >}}

In the server configuration options, check the **Enable** box.

Choose **Semtech** as the **Type**.

For the **Server Address** choose **custom**, and enter the address of {{% tts %}} deployment you are using. See [Server Addresses]({{< ref "/getting-started/server-addresses" >}}) section for help.

Choose the appropriate **Port Up** and **Port Down** values. These are both **1700** by default in {{% tts %}}.

Click **Save** to continue.

{{< figure src="../semtech.png" alt="Semtech Configuration" >}}

If your configuration was successful, your gateway will connect to {{% tts %}} after a couple of seconds.