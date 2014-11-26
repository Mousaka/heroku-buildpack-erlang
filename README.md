## Heroku buildpack: Erlang (forked from https://github.com/archaelus/heroku-buildpack-erlang)

This is a Heroku buildpack for Erlang apps. It uses [erlang.mk](https://github.com/ninenines/erlang.mk).

###NOTE
Not sure this works yet. I'm able to build my heroku project but it's having trouble starting the application:

	heroku[web.1]: Starting process with command `./_rel/gatherl_release/bin/gatherl_release start`
	app[web.1]: egrep: /app/_rel/gatherl_release/releases/1/vm.args: No such file or directory

Might also be that my app projects Procfile is not written correctly, currently being:

	web: ./_rel/gatherl_release/bin/gatherl_release start

### Configure your Heroku App

    $ heroku config:add BUILDPACK_URL="https://github.com/Mousaka/heroku-buildpack-erlang.git" -a YOUR_APP

or
    $ heroku create --buildpack "https://github.com/Mousaka/heroku-buildpack-erlang.git"

### Select an Erlang version

The Erlang/OTP release version that will be used to build and run your application is now sourced from a dotfile called `.preferred_otp_version`. It needs to be the branch or tag name from the http://github.com/erlang/otp repository, and further, needs to be one of the versions that precompiled binaries are available for.

Currently supported OTP versions:

* master (R17B pre)
* master-pu (R16B pre)
* OTP_R15B
* OTP_R15B01
* OTP_R15B02
* OTP_R16B
* OTP_R16B01
* OTP_R16B02
* OTP_R16B03

To select the version for your app:

    $ echo OTP_R15B01 > .preferred_otp_version
    $ git commit -m "Select R15B01 as preferred OTP version" .preferred_otp_version

### Build your Heroku App

    $ git push heroku master

You may need to write a new commit and push if your code was already up to date.
