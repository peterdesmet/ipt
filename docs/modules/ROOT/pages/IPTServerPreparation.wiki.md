# How To Prepare Your IPT Server

## Introduction

Since the IPT ships as a `.war` file, installing the IPT consists of deploying the `.war` file in a servlet container such as Tomcat.

This page explains how to install different types of servlet containers on your server, and how to deploy the IPT in them.

It isn't necessary to use an Apache reverse proxy, but in case you do, this page also explains how to configure an Apache virtual host declaration for the IPT.

## Servlet Containers

The most common servlet containers used to deploy the IPT are Tomcat, Jetty and Wildfly8 (JBoss). Information about how to deploy the IPT in these servlets follows.

### Tomcat

The IPT has been tested and works well with Tomcat 8.0 and 9.0. The Apache Tomcat documentation can be found on http://tomcat.apache.org/. Also, minimal instructions for Tomcat installations on various operating systems can be found in associated Server Preparation pages:

  * [Tomcat on Mac OS X](TomcatInstallationMacOSX.wiki)
  * [Tomcat on Windows 7](TomcatInstallationWindows7.wiki)
  * [Tomcat on Windows 8](TomcatInstallationWindows8.wiki)
  * [Tomcat on Linux](TomcatInstallationLinux.wiki)

Download the `ipt.war` file of the latest release of the IPT from https://www.gbif.org/ipt. Copy the `ipt.war` file to the Tomcat webapps folder and then start Tomcat, or restart Tomcat if it is already running. You can then invoke the IPT in a web browser running on the same server by using the following URL: http://localhost:8080/ipt

If the installation doesn't start please check the `catalina.out` logfile, and refer to the [FAQ](FAQ.md) for help.

The following screencast also explains how to install the IPT using Tomcat, assuming Tomcat has already been installed.

<a href="https://vimeo.com/116142276" target="_blank"><img src="https://i.vimeocdn.com/video/502401133_640.jpg" alt="How to install the IPT screencast" width="640" height="384" border="10" /></a>

### Jetty

*As a very rough guide, on CentOS:*
```
yum install jetty-runner
java -jar /usr/share/java/jetty/jetty-runner.jar --port 8080 ipt.war
```

### Wildfly8 (JBoss)

Instructions pending. (Unlikely to be written by the IPT developers.)

## Linux packages

As an alternative to installing a servlet container and adding the `ipt.war`, [issue 1304](https://github.com/gbif/ipt/issues/1304#issuecomment-261311424) shows using CentOS (or RedHat) packages to install the IPT.  Please comment on the issue if you find these useful.

## Opening the IPT to the Internet

You will probably need to work with your system or network administrator for the IPT to be available on the Internet.

You will need a DNS name for the server ("`ipt.example.org`") and the firewall to allow access.

Many people use Apache as a proxy, often to allow sharing other websites on the same server or HTTPS access.

The configuration used by `ipt.gbif.org` is shown here as an example.  It uses Apache HTTPD, with the `mod_proxy` module installed. The paths `/media` and `/icons` are excluded from being passed to the IPT, to allow hosting static image files (e.g. occurrence images) on the same server.  Requests to http://ipt.gbif.org/ are redirected to the secure https://ipt.gbif.org/.

```
<VirtualHost *:80>
        ServerName                 ipt.gbif.org
        ServerAdmin                webmaster@gbif.org
        ErrorLog                   logs/ipt-80_error
        CustomLog                  logs/ipt-80_log combined

        Redirect                   / https://ipt.gbif.org/
</VirtualHost>

<VirtualHost *:443>
        ServerName                 ipt.gbif.org
        ServerAdmin                webmaster@gbif.org
        ErrorLog                   logs/ipt-443_error
        CustomLog                  logs/ipt-443_log combined

        DocumentRoot               /var/www/html/ipt

        Options                    +Indexes
        AddDefaultCharset          UTF-8

        ProxyPreserveHost          On
        ProxyPass                  /icons !
        ProxyPass                  /media !
        ProxyPass                  / http://localhost:8080/ipt/
        ProxyPassReverse           / http://localhost:8080/ipt/
        ProxyPassReverseCookiePath /ipt /

        SSLEngine                  On
        # Other SSL configuration (certificates etc)
</VirtualHost>
```