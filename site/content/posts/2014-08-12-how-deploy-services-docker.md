---
title: How to deploy services using docker
author: Tiphaine
date: 2014-08-12T09:10:00+00:00
featured_image: /wp-content/uploads/2014/08/Sogilis-Christophe-Levet-Photographe-7517.jpg
tumblr_sogilisblog_permalink:
  - http://sogilisblog.tumblr.com/post/94520400771/how-to-deploy-services-using-docker
tumblr_sogilisblog_id:
  - 94520400771
pyre_show_first_featured_image:
  - no
pyre_portfolio_width_100:
  - default
pyre_image_rollover_icons:
  - default
pyre_post_links_target:
  - no
pyre_related_posts:
  - default
pyre_share_box:
  - default
pyre_post_pagination:
  - default
pyre_author_info:
  - default
pyre_post_meta:
  - default
pyre_post_comments:
  - default
pyre_slider_position:
  - default
pyre_slider_type:
  - no
pyre_avada_rev_styles:
  - default
pyre_display_header:
  - yes
pyre_header_100_width:
  - default
pyre_header_bg_full:
  - no
pyre_header_bg_repeat:
  - repeat
pyre_displayed_menu:
  - default
pyre_display_footer:
  - default
pyre_display_copyright:
  - default
pyre_footer_100_width:
  - default
pyre_sidebar_position:
  - default
pyre_page_bg_layout:
  - default
pyre_page_bg_full:
  - no
pyre_page_bg_repeat:
  - repeat
pyre_wide_page_bg_full:
  - no
pyre_wide_page_bg_repeat:
  - repeat
pyre_page_title:
  - default
pyre_page_title_text:
  - default
pyre_page_title_text_alignment:
  - default
pyre_page_title_100_width:
  - default
pyre_page_title_bar_bg_full:
  - default
pyre_page_title_bg_parallax:
  - default
pyre_page_title_breadcrumbs_search_bar:
  - default
fusion_builder_status:
  - inactive
avada_post_views_count:
  - 7768
sbg_selected_sidebar:
  - 'a:1:{i:0;s:1:"0";}'
sbg_selected_sidebar_replacement:
  - 'a:1:{i:0;s:0:"";}'
sbg_selected_sidebar_2:
  - 'a:1:{i:0;s:1:"0";}'
sbg_selected_sidebar_2_replacement:
  - 'a:1:{i:0;s:0:"";}'
categories:
  - DÉVELOPPEMENT
tags:
  - debian
  - deployment
  - docker
  - en

---
**Why would you use docker to deploy services when there are many configuration management tools such as puppet, chef or cfengine. While these tools are a great evolution from doing everything manually, they are not separating clearly between the configuration of your system (your domain, user accounts) and the installation and integration of services together**.

&nbsp;

Docker is a container solution. You manage your services as binary images (built from a `Dockerfile` script). The idea is that container images won’t contain configuration that is too specific. Regenerating whole binary images if you want to flip a boolean value is not a good idea. You’ll have then to think how you can build generic images and put your configuration outside.

Docker has also the advantage of being reproducible. You can easily take your container disk image and put it on another server for backups, or migration to another host. Application are separated from each other and security is improved. You can now install PHP applications on your server without fear.

&nbsp;

<!-- more -->

## **Docker service example: a mail server and its webmail**

An example of service could be a mail server and its webmail. I decided to split this in two containers: docker-mail containing the SMTP (exim) and IMAP (dovecot) server, and the PHP webmail on another container. The advantage to split there is security. The SMTP and IMAP server are on the same container for simplicity because these two are interdependent and talk with each other using file sockets.

When you run these services you need both static configuration that will never change and be common to all instances of these services, and dynamic configuration that can change between instances.

### **<span style="text-decoration: underline;">Static configuration</span>**

Static configuration is bundled within the docker image, and is specified in the `Dockerfile`, the recipe that builds the images. It includes:

  * package installation
  * socket configuration for communication between dovecot (the IMAP server) and exim (the SMTP/submission server)
  * default configuration for both SMTP and IMAP
  * virtual host configuration for the webmail

### **<span style="text-decoration: underline;">Dynamic configuration</span>**

Dynamic configuration is a little more complicated. I believe it should be minimal and most of the choices should be bundled within the disk image itself. What you are likely to find here is:

  * domain names for which the mail server accepts mail for
  * domain names for which the mail server is relaying mail
  * user database (the choice was to have a passwd-like file containing the user database, but a more complete setup would have this changed to connect to another container providing authentication such as a LDAP server or a database)
  * address of the mail server for the webmail

Then, how can dynamic configuration can be specified? Docker provides a few tools:

  * command line arguments when starting the container
  * environment variables set on the container
  * linked containers. A container (the webmail) can be linked to another (the mail server). The network interfaces of the mail server will be exposed within the webmail container. The hostname and ports of the linked containers are found in environment variables and the `/etc/hosts` file.
  * when starting a container, docker can run a specified file (generally a shell script) that use the information above to configure the container at startup.

This works well for everything except for the user file list. Notice that if an authentication container existed, we could link it into the mail container and it would work very well. In that case, we’ll see later that we can setup a ssh access to enter the container. Once inside, we can add a user using standard unix commands.

The code:

  * <span style="text-decoration: underline;"><a href="https://github.com/mildred/docker-mail" target="_blank">docker-mail on github</a></span>
  * <span style="text-decoration: underline;"><a href="https://github.com/mildred/docker-roundcube" target="_blank">docker-roundcube on github</a></span>

&nbsp;

## **How to have docker containers always running**

Docker by default is restarting containers at startup that were running at shutdown. This is a good feature but isn’t really a good solution when you want to ensure the container is always running. There are many ways the docker container could not be restarted.

You’ll have to configure <span style="text-decoration: underline;"><a href="https://docs.docker.com/articles/host_integration/" target="_blank">host integration</a></span>. This is the only reliable way to do it. It requires writing a service file (for either systemd, upstart or sysvinit) and installing it. This is not strainghtfoward either.

### **<span style="text-decoration: underline;">Gear from OpenShift</span>**

There is a tool called <span style="text-decoration: underline;"><a href="https://openshift.github.io/geard/" target="_blank">geard</a></span> from the OpenShift project. It seems perfect for the task we have. It is a daemon that ensures that the docker services you want are always running and managed by systemd. It provides a JSON file format to describe how to provision a few docker containers running together. It manages docker volumes in separate images so you can keep backups or change the system image and keep your data.

The JSON deployment file looks like:

<pre class="wp-code-highlight prettyprint">{
  "Keys":[{
    "Type": "authorized_keys",
    "Value": "ssh-rsa ..."
  }],
 "containers":[
    {
      "name":"mail",
      "count":1,
      "image":"mildred/exim-dovecot-mail",
      "publicports":[
        {"internal":4190, "external":4190},
        {"internal":25, "external":25},
        {"internal":993, "external":993},
        {"internal":143, "external":143},
        {"internal":465, "external":465},
        {"internal":587, "external":587}
      ],
      "environment": [
        {"name": "LOCAL_DOMAINS", "value": "example.org"}
      ]
    },
    {
      "name":"roundcube",
      "count":1,
      "image":"mildred/roundcube",
      "links":[{"to":"mail"}],
      "publicports":[{"internal":443, "external":4443}]
    }
  ]
}
</pre>

Moreover, it lets you specify ssh keys for your containers, and set up the ssh daemon so these ssh keys can let you in the containers directly. `ssh container-name@host` will provide you a shell on the container `container-name` running on `host`.

Unfortunately, it is not really supposed to be run on its own on a debian host (<span style="text-decoration: underline;"><a href="https://gist.github.com/mildred/4e32276fc197395f0f81" target="_blank">although it could be done</a></span>) and the ssh feature doesn’t work unless containers are isolated. Isolation changes the script that is run by the container at startup and it breaks things.

On top of this, the deployment JSON file is not documented anywhere.

### **<span style="text-decoration: underline;">Deploy Manually</span>**

Gear has a great way to do this, we could always do the same things manually, in a declarative format. To simplify things the most, I came up with a shell script that I run on the server and that does the same provisioning as the JSON file above:

<pre class="wp-code-highlight prettyprint">name=example
LOCAL_DOMAINS=example.org
ssh_key="ssh-rsa ..."

docker pull mildred/exim-dovecot-mail
docker pull mildred/roundcube

docker-unit $name-mail      "-p 4190:4190 -p 25:25 -p 993:993 -p 143:143 -p 465:465 -p 587:587 -e
"LOCAL_DOMAINS=$LOCAL_DOMAINS" mildred/exim-dovecot-mail"
docker-unit $name-roundcube "-p 4443:443 --link "$name-mail:mail" mildred/roundcube"
docker-ssh  $name-mail      "$ssh_key"
docker-ssh  $name-roundcube "$ssh_key"

systemctl enable $name-mail
systemctl enable $name-roundcube
systemctl start $name-mail
systemctl start $name-roundcube
</pre>

There is however a few things to execute first and some shell functions to define. However I like this solution the most because the configuration (the three variables at the top) is separated from the code that run the deployment.

How is that implemented? Following <span style="text-decoration: underline;"><a href="https://docs.docker.com/articles/host_integration/" target="_blank">host integration</a></span> you have to ensure a few things on your host system:

  * that you are running systemd: <pre class="wp-code-highlight prettyprint">DEBIAN_FRONTEND=noninteractive apt-get install -y systemd systemd-sysv
</pre>

  * that docker will not try to restart containers: <pre class="wp-code-highlight prettyprint">echo &#039;DOCKER_OPTS="-r=false"&#039; &gt; /etc/default/docker
</pre>

  * and that you have the `nsenter` command to get a shell within a running container: <pre class="wp-code-highlight prettyprint">docker run --rm -v /usr/local/bin:/target jpetazzo/nsenter
</pre>

**Instantiate a container**

Once you have all that, let’s see how these shell functions are implemented. The function `docker-unit NAME ARGS` is there to declare a new instance of a container. It takes the instance name (`NAME`) and the docker arguments (`ARGS`) given to `docker run`. Its job is to create a systemd unit file, and that’s what it does literally:

<pre class="wp-code-highlight prettyprint">docker-unit(){
  local name="$1"
  shift
  local filename="/etc/systemd/system/$name.service"
  cat &gt;"$filename" &lt;&lt;EOF
[Unit]
Description=Container $name
After=docker.service

[Service]
Restart=always
ExecStart=/usr/local/bin/docker-start-run $name $@
ExecStop=/usr/bin/docker stop -t 2 $name

[Install]
WantedBy=local.target
EOF
}
</pre>

You can see that the `ExecStart` command is running `/usr/local/bin/docker-start-run`. This file is a shell script that spawn the docker container, ensuring that the volumes are from another container `$name-data` (so they can be backuped easily). Its code is:

<pre class="wp-code-highlight prettyprint">#!/bin/bash

name="$1"
shift

if ! /usr/bin/docker inspect --format="Reusing {{.ID}}" "$name-data" 2&gt;/dev/null; then
  docker run --name "$name-data" --volumes-from "$name-data" --entrypoint /bin/true "$@"
fi

/usr/bin/docker rm "$name"
exec /usr/bin/docker run --rm --attach=stdout --attach=stderr --name="$name" --volumes-from="$name-data" "$@"
</pre>

This could actually be inserted within the unit file (and that&rsquo;w what gear does). From this code you can see that the container is recreated anew each time the service is restarted. The container must be designed such as all persistent data is declared in a volume. This persistent data will be put in the `*-data` container and it is the only thing that persists.

The reason why you don’t want to have a persistent container is because at some point you’ll have to update your container. You don’t run `apt-get update` within the container, rather you build a new image and use it instead. At that time, you’ll be forced to drop all your changes. Better do it early and not rely on persistent storage.

**Install ssh access**

Using gear, ssh access is managed by configuring the ssh daemon using `AuthorizedKeysCommand /usr/sbin/gear-auth-keys-command` and `AuthorizedKeysCommandUser nobody`. When a ssh connection is made, `gear-auth-keys-command` is executed and can grant access. The problem is that the user id will be `nobody` and won’t have the permission to execute `nsenter` (because the container is running a root user).

What I did instead is create a user on the system with uid 0 for each container instance. And setup the `authorized_keys` file to execute `nsenter`. This may need to be improved.

And this is how `docker-ssh` is implemented:

<pre class="wp-code-highlight prettyprint">docker-ssh(){ local user="$1" local name="$1" local shell="/bin/bash" shift while true; do case "$1" in -u*) user="${1#-?}" ;; -s*) shell="${1#-?}" ;; --user=*) user="${1#-*=}" ;; --shell=*) shell="${1#-*=}" ;; *) break ;; esac shift done [ "${shell////}" = "$shell" ] &amp;&amp; shell="/bin/$shell" local ssh_key="$*" if uid="$(id -u "$user" 2&gt;/dev/null)"; then if [ "0$uid" = 00 ]; then echo "Using existing user $user for ssh access" else echo "Existing user $user cannot be used for ssh access (uid $uid should be 0)" &gt;&amp;2 return 1 fi else echo "Creating user $user for ssh access" useradd -d /home/$user -N -m -o -u 0 $user fi mkdir -p /home/$user/.ssh chown -R $user /home/$user ( fgrep -v "$ssh_key" /home/$user/.ssh/authorized_keys 2&gt;/dev/null echo "command="nsenter --target $(docker inspect --format {{.State.Pid}} $name) --mount --uts --ipc --net --pid $shell" $ssh_key" ) | sort | uniq &gt;/home/$user/.ssh/authorized_keys- mv /home/$user/.ssh/authorized_keys- /home/$user/.ssh/authorized_keys }</pre>

`<br />
<strong>Shanti</strong>`