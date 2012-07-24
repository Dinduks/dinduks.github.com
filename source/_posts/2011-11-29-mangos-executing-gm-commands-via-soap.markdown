---
comments: true
date: 2011-11-29 01:10:03
layout: post
slug: mangos-executing-gm-commands-via-soap
title: 'MaNGOS: executing GM commands via SOAP'
categories:
- Development
- Pieces of code
- Tutorials
tags:
- mangos
- php
- soap
- trinity
---

Hi,

I have recently built a site for a World of Warcraft server using **Symfony2** framework.
Among the features I had to implement, there was a shop where donators can buy rewards, such as levels, gold, items and teleportations.

During my first reflexions, as a Web developer who has no knownledge about MaNGOS server, I thought of rewarding players by adding or updating data in the database. I started experimenting that way, but I quickly realized that it was leading me nowhere.

There are some reasons why:

* Adding levels using the database is useless if the player is online. Because it doesn't apply instantly and once the player logs off, the server will override the level in the database with the player's level on the logout.
* The samething applies for teleportation.
* Sending an item: I won't give much details because it's too complicated, but basically, sending an item using the database is a pain in the ass since it requires creating many rows here and there. Some of these rows are in tables with non-documented columns, which make them (almost) impossible to create. *#mindfuck*

As you may already know if you're familiar with MaNGOS, all the actions mentionned above are doable using GM commands.
Fortunately, MaNGOS server already has a SOAP Web Service allowing to execute GM commands directly on the server.
Using it will not only allow you to do things quickly and easily, but it is also safe since you know that MaNGOS native commands will do the what you ask them the right way.

### This is how to use SOAP with PHP:

#### Enable SOAP
First of all, make sure to have the SOAP extension enabled: *extension=php_soap.dll* on Windows.

#### Store your server's info in variables:

    $soapUsername = 'mangos_usr';
    $soapPassword = 'mangos_pwd';
    $soapHost = '127.0.0.1';
    $soapPort = '7878';

#### Then create an instance of SoapClient and pass to it the required parameters

    $client = new SoapClient(NULL, array(
        'location' => "http://$soapHost:$soapPort/",
        'uri'      => 'urn:MaNGOS',
        'style'    => SOAP_RPC,
        'login'    => $soapUsername,
        'password' => $soapPassword,
    ));

The login and the passwords are the ones that you use to log into your GM account.

#### Create a command

    $command = "character level Dinduks 70";

Note that your command musn't start with a dot.

#### Execute that command

    $result = $client->executeCommand(new SoapParam($command, 'command'));

`$result` will contain the same text that you'd see in yellow color if you did execute the command in game.

It's as simple as that!

#### Bonus

I wrote a short script that allows to execute GM commands from a command prompt. It's pretty funny and can be useful if you want to do something without starting an instance of the game.
You can grab the script on Github: [GM-Commands-Script](https://github.com/Dinduks/GM-Commands-Script)

Have fun!
