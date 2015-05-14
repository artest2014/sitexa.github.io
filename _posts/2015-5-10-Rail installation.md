---
layout: post
title: Rails v4.2 - installation
category: 'ecommerce'
---

##0,installation with gem install rails

    $ sudo gem install rails

这个命令将在/var/lib/gems/2.2.0/中安装rails 4.2.1及相关的组件包。

    Fetching: rails-deprecated_sanitizer-1.0.3.gem (100%)
    Successfully installed rails-deprecated_sanitizer-1.0.3
    Fetching: rails-dom-testing-1.0.6.gem (100%)
    Successfully installed rails-dom-testing-1.0.6
    Fetching: loofah-2.0.2.gem (100%)
    Successfully installed loofah-2.0.2
    Fetching: rails-html-sanitizer-1.0.2.gem (100%)
    Successfully installed rails-html-sanitizer-1.0.2
    Fetching: erubis-2.7.0.gem (100%)
    Successfully installed erubis-2.7.0
    Fetching: builder-3.2.2.gem (100%)
    Successfully installed builder-3.2.2
    Fetching: actionview-4.2.1.gem (100%)
    Successfully installed actionview-4.2.1
    Fetching: rack-1.6.1.gem (100%)
    Successfully installed rack-1.6.1
    Fetching: rack-test-0.6.3.gem (100%)
    Successfully installed rack-test-0.6.3
    Fetching: actionpack-4.2.1.gem (100%)
    Successfully installed actionpack-4.2.1
    Fetching: sprockets-3.0.3.gem (100%)
    Successfully installed sprockets-3.0.3
    Fetching: sprockets-rails-2.3.0.gem (100%)
    Successfully installed sprockets-rails-2.3.0
    Fetching: thor-0.19.1.gem (100%)
    Successfully installed thor-0.19.1
    Fetching: railties-4.2.1.gem (100%)
    Successfully installed railties-4.2.1
    Fetching: globalid-0.3.5.gem (100%)
    Successfully installed globalid-0.3.5
    Fetching: activejob-4.2.1.gem (100%)
    Successfully installed activejob-4.2.1
    Fetching: mime-types-2.5.gem (100%)
    Successfully installed mime-types-2.5
    Fetching: mail-2.6.3.gem (100%)
    Successfully installed mail-2.6.3
    Fetching: actionmailer-4.2.1.gem (100%)
    Successfully installed actionmailer-4.2.1
    Fetching: arel-6.0.0.gem (100%)
    Successfully installed arel-6.0.0
    Fetching: activemodel-4.2.1.gem (100%)
    Successfully installed activemodel-4.2.1
    Fetching: activerecord-4.2.1.gem (100%)
    Successfully installed activerecord-4.2.1
    Fetching: rails-4.2.1.gem (100%)
    Successfully installed rails-4.2.1
    Parsing documentation for rails-deprecated_sanitizer-1.0.3
    Installing ri documentation for rails-deprecated_sanitizer-1.0.3
    Parsing documentation for rails-dom-testing-1.0.6
    Installing ri documentation for rails-dom-testing-1.0.6
    Parsing documentation for loofah-2.0.2
    Installing ri documentation for loofah-2.0.2
    Parsing documentation for rails-html-sanitizer-1.0.2
    Installing ri documentation for rails-html-sanitizer-1.0.2
    Parsing documentation for erubis-2.7.0
    Installing ri documentation for erubis-2.7.0
    Parsing documentation for builder-3.2.2
    Installing ri documentation for builder-3.2.2
    Parsing documentation for actionview-4.2.1
    Installing ri documentation for actionview-4.2.1
    Parsing documentation for rack-1.6.1
    Installing ri documentation for rack-1.6.1
    Parsing documentation for rack-test-0.6.3
    Installing ri documentation for rack-test-0.6.3
    Parsing documentation for actionpack-4.2.1
    Installing ri documentation for actionpack-4.2.1
    Parsing documentation for sprockets-3.0.3
    Installing ri documentation for sprockets-3.0.3
    Parsing documentation for sprockets-rails-2.3.0
    Installing ri documentation for sprockets-rails-2.3.0
    Parsing documentation for thor-0.19.1
    Installing ri documentation for thor-0.19.1
    Parsing documentation for railties-4.2.1
    Installing ri documentation for railties-4.2.1
    Parsing documentation for globalid-0.3.5
    Installing ri documentation for globalid-0.3.5
    Parsing documentation for activejob-4.2.1
    Installing ri documentation for activejob-4.2.1
    Parsing documentation for mime-types-2.5
    Installing ri documentation for mime-types-2.5
    Parsing documentation for mail-2.6.3
    Installing ri documentation for mail-2.6.3
    Parsing documentation for actionmailer-4.2.1
    Installing ri documentation for actionmailer-4.2.1
    Parsing documentation for arel-6.0.0
    Installing ri documentation for arel-6.0.0
    Parsing documentation for activemodel-4.2.1
    Installing ri documentation for activemodel-4.2.1
    Parsing documentation for activerecord-4.2.1
    Installing ri documentation for activerecord-4.2.1
    Parsing documentation for rails-4.2.1
    Installing ri documentation for rails-4.2.1

    Done installing documentation for rails-deprecated_sanitizer, rails-dom-testing, loofah, rails-html-sanitizer, erubis, builder, actionview, rack, rack-test, actionpack, sprockets, sprockets-rails, thor, railties, globalid, activejob, mime-types, mail, actionmailer, arel, activemodel, activerecord, rails after 444 seconds
    23 gems installed

查看rails版本
    $ rails -v
    $ rails 4.2.1


##1,Create your application skeleton

    rails new railsapp1

安装结果

          creat         create  README.rdoc
          create  Rakefile
          create  config.ru
          create  .gitignore
          create  Gemfile
          create  app
          create  app/assets/javascripts/application.js
          create  app/assets/stylesheets/application.css
          create  app/controllers/application_controller.rb
          create  app/helpers/application_helper.rb
          create  app/views/layouts/application.html.erb
          create  app/assets/images/.keep
          create  app/mailers/.keep
          create  app/models/.keep
          create  app/controllers/concerns/.keep
          create  app/models/concerns/.keep
          create  bin
          create  bin/bundle
          create  bin/rails
          create  bin/rake
          create  bin/setup
          create  config
          create  config/routes.rb
          create  config/application.rb
          create  config/environment.rb
          create  config/secrets.yml
          create  config/environments
          create  config/environments/development.rb
          create  config/environments/production.rb
          create  config/environments/test.rb
          create  config/initializers
          create  config/initializers/assets.rb
          create  config/initializers/backtrace_silencers.rb
          create  config/initializers/cookies_serializer.rb
          create  config/initializers/filter_parameter_logging.rb
          create  config/initializers/inflections.rb
          create  config/initializers/mime_types.rb
          create  config/initializers/session_store.rb
          create  config/initializers/wrap_parameters.rb
          create  config/locales
          create  config/locales/en.yml
          create  config/boot.rb
          create  config/database.yml
          create  db
          create  db/seeds.rb
          create  lib
          create  lib/tasks
          create  lib/tasks/.keep
          create  lib/assets
          create  lib/assets/.keep
          create  log
          create  log/.keep
          create  public
          create  public/404.html
          create  public/422.html
          create  public/500.html
          create  public/favicon.ico
          create  public/robots.txt
          create  test/fixtures
          create  test/fixtures/.keep
          create  test/controllers
          create  test/controllers/.keep
          create  test/mailers
          create  test/mailers/.keep
          create  test/models
          create  test/models/.keep
          create  test/helpers
          create  test/helpers/.keep
          create  test/integration
          create  test/integration/.keep
          create  test/test_helper.rb
          create  tmp/cache
          create  tmp/cache/assets
          create  vendor/assets/javascripts
          create  vendor/assets/javascripts/.keep
          create  vendor/assets/stylesheets
          create  vendor/assets/stylesheets/.keep
             run  bundle install
    Enter your password to install the bundled RubyGems to your system:
    Fetching gem metadata from https://rubygems.org/............
    Fetching gem metadata from https://rubygems.org/..
    Resolving dependencies...
    Using rake (10.4.2)
    Using i18n (0.7.0)
    Using json (1.8.2)
    Installing minitest (5.6.1)
    Using thread_safe (0.3.5)
    Using tzinfo (1.2.2)
    Using activesupport (4.2.1)
    Using builder (3.2.2)
    Using erubis (2.7.0)
    Using mini_portile (0.6.2)
    Using nokogiri (1.6.6.2)
    Using rails-deprecated_sanitizer (1.0.3)
    Using rails-dom-testing (1.0.6)
    Using loofah (2.0.2)
    Using rails-html-sanitizer (1.0.2)
    Using actionview (4.2.1)
    Using rack (1.6.1)
    Using rack-test (0.6.3)
    Using actionpack (4.2.1)
    Using globalid (0.3.5)
    Using activejob (4.2.1)
    Using mime-types (2.5)
    Using mail (2.6.3)
    Using actionmailer (4.2.1)
    Using activemodel (4.2.1)
    Using arel (6.0.0)
    Using activerecord (4.2.1)
    Installing debug_inspector (0.0.2)
    Installing binding_of_caller (0.7.2)
    Using bundler (1.3.5)
    Installing columnize (0.9.0)
    Installing byebug (4.0.5)
    Installing coffee-script-source (1.9.1.1)
    Installing execjs (2.5.2)
    Using coffee-script (2.4.1)
    Using thor (0.19.1)
    Using railties (4.2.1)
    Installing coffee-rails (4.1.0)
    Installing multi_json (1.11.0)
    Installing jbuilder (2.2.13)
    Installing jquery-rails (4.0.3)
    Using sprockets (3.0.3)
    Using sprockets-rails (2.3.0)
    Using rails (4.2.1)
    Using rdoc (4.2.0)
    Using sass (3.4.13)
    Installing tilt (1.4.1)
    Installing sass-rails (5.0.3)
    Installing sdoc (0.4.1)
    Installing spring (1.3.6)
    Installing sqlite3 (1.3.10)
    Installing turbolinks (2.5.3)
    Installing uglifier (2.7.1)
    Installing web-console (2.1.2)
    Your bundle is complete!
    Use `bundle show [gemname]` to see where a bundled gem is installed.
             run  bundle exec spring binstub --all
    * bin/rake: spring inserted
    * bin/rails: spring inserted

##2,Run you application

    cd railsapp1
    rails server

see rult:

    Warning: Running `gem pristine --all` to regenerate your installed gemspecs (and deleting then reinstalling your bundle if you use bundle --path) will improve the startup performance of Spring.
    => Booting WEBrick
    => Rails 4.2.1 application starting in development on http://localhost:3000
    => Run `rails server -h` for more startup options
    => Ctrl-C to shutdown server
    [2015-05-10 10:52:25] INFO  WEBrick 1.3.1
    [2015-05-10 10:52:25] INFO  ruby 2.2.2 (2015-04-13) [x86_64-linux-gnu]
    [2015-05-10 10:52:25] INFO  WEBrick::HTTPServer#start: pid=11888 port=3000


open your browser:

    http://localhost:3000

see result:

<img src="/images/rubyonrails.png"/>

run gem pristine --all

    Restoring gems to pristine condition...
    Building native extensions.  This could take a while...
    Restored RedCloth-4.2.9
    Restored actionmailer-4.2.1
    Restored actionpack-4.2.1
    Restored actionview-4.2.1
    Restored activejob-4.2.1
    Restored activemodel-4.2.1
    Restored activerecord-4.2.1
    Restored activesupport-4.2.1
    Restored arel-6.0.0
    Skipped bigdecimal-1.2.6, it is a default gem
    Building native extensions.  This could take a while...
    Restored binding_of_caller-0.7.2
    Restored blankslate-2.1.2.4
    Restored builder-3.2.2
    Restored bundler-1.9.2
    Building native extensions.  This could take a while...
    Restored byebug-4.0.5
    Restored celluloid-0.16.0
    Restored classifier-reborn-2.0.3
    Restored coffee-rails-4.1.0
    Restored coffee-script-2.4.1
    Restored coffee-script-source-1.9.1.1
    Restored coffee-script-source-1.9.1
    Restored colorator-0.1
    Restored columnize-0.9.0
    Building native extensions.  This could take a while...
    Restored debug_inspector-0.0.2
    Building native extensions.  This could take a while...
    Restored duktape-1.1.2.0
    Restored erubis-2.7.0
    Restored execjs-2.5.2
    Restored execjs-2.5.1
    Building native extensions.  This could take a while...
    Restored fast-stemmer-1.0.2
    Building native extensions.  This could take a while...
    Restored ffi-1.9.8
    Restored gemoji-2.1.0
    Restored github-pages-34
    Restored github-pages-health-check-0.2.2
    Restored globalid-0.3.5
    Building native extensions.  This could take a while...
    Restored hitimes-1.2.2
    -------------------------------------------------
    Thank you for installing html-pipeline!
    You must bundle Filter gem dependencies.
    See html-pipeline README.md for more details.
    https://github.com/jch/html-pipeline#dependencies
    -------------------------------------------------
    Restored html-pipeline-1.9.0
    Restored i18n-0.7.0
    Skipped io-console-0.4.3, it is a default gem
    Restored jbuilder-2.2.13
    Restored jekyll-2.4.0
    Restored jekyll-coffeescript-1.0.1
    Restored jekyll-gist-1.2.1
    Restored jekyll-mentions-0.2.1
    Restored jekyll-paginate-1.1.0
    Restored jekyll-redirect-from-0.6.2
    Restored jekyll-sass-converter-1.2.0
    Restored jekyll-sitemap-0.8.1
    Restored jekyll-watch-1.2.1
    Restored jemoji-0.4.0
    Restored jquery-rails-4.0.3
    Building native extensions.  This could take a while...
    Restored json-1.8.2
    Skipped json-1.8.1, it is a default gem
    Restored kramdown-1.5.0
    Restored libv8-3.16.14.7-x86_64-linux
    Restored liquid-2.6.1
    Restored listen-2.10.0
    Restored loofah-2.0.2
    Restored mail-2.6.3
    Restored maruku-0.7.0
    Restored mercenary-0.3.5
    Restored mime-types-2.5
    Restored mini_portile-0.6.2
    Restored minitest-5.6.1
    Restored minitest-5.5.1
    Restored multi_json-1.11.0
    Restored net-dns-0.8.0
    Building native extensions.  This could take a while...
    Restored nokogiri-1.6.6.2
    Restored parslet-1.5.0
    Building native extensions.  This could take a while...
    Restored posix-spawn-0.3.11
    Skipped psych-2.0.8, it is a default gem
    Restored public_suffix-1.5.0
    Restored pygments.rb-0.6.1
    Restored rack-1.6.1
    Restored rack-test-0.6.3
    Restored rails-4.2.1
    Restored rails-deprecated_sanitizer-1.0.3
    Restored rails-dom-testing-1.0.6
    Restored rails-html-sanitizer-1.0.2
    Restored railties-4.2.1
    Skipped rake-10.4.2, it is a default gem
    Restored rb-fsevent-0.9.4
    Restored rb-inotify-0.9.5
    Building native extensions.  This could take a while...
    Restored rdiscount-2.1.7
    Skipped rdoc-4.2.0, it is a default gem
    Building native extensions.  This could take a while...
    Restored redcarpet-3.1.2
    Restored ref-1.0.5
    Restored safe_yaml-1.0.4
    Restored sass-3.4.13
    Restored sass-rails-5.0.3
    Restored sdoc-0.4.1
    Restored spring-1.3.6
    Restored sprockets-3.0.3
    Restored sprockets-rails-2.3.0
    Building native extensions.  This could take a while...
    Restored sqlite3-1.3.10
    Restored terminal-table-1.4.5
    Building native extensions.  This could take a while...
    Restored therubyracer-0.12.2
    Restored therubyrhino-2.0.4
    Restored therubyrhino_jar-1.7.4
    Restored thor-0.19.1
    Restored thread_safe-0.3.5
    Restored tilt-1.4.1
    Restored timers-4.0.1
    Restored toml-0.1.2
    Restored turbolinks-2.5.3
    Restored tzinfo-1.2.2
    Restored uglifier-2.7.1
    Restored web-console-2.1.2
    Building native extensions.  This could take a while...
    Restored yajl-ruby-1.2.1

restart rails server:

    rails server

<img src="/images/rubyonrails-env.png" />

##3,Install sqlite3

    sudo gem install sqlite3

see result:

    Building native extensions.  This could take a while...
    Successfully installed sqlite3-1.3.10
    Parsing documentation for sqlite3-1.3.10
    Installing ri documentation for sqlite3-1.3.10
    Done installing documentation for sqlite3 after 0 seconds
    1 gem installed

##4, install ror_ecommerce by RubyMine

    clone source :https://github.com/drhenner/ror_ecommerce.git

copy config/database.yml.sqlite3 config/database.yml

    cp config/database.yml.sqlite3 config/database.yml

Install gems and build the app:

    gem install bundler

    result:
    Successfully installed bundler-1.9.6
    Parsing documentation for bundler-1.9.6
    Done installing documentation for bundler after 3 seconds
    1 gem installed

    bundle install
    Fetching gem metadata from http://rubygems.org/.............
    Fetching version metadata from http://rubygems.org/...
    Fetching dependency metadata from http://rubygems.org/..
    Fetching git://github.com/drhenner/authlogic.git
    Using rake 10.4.2
    Installing Ascii85 1.0.2
    Installing CFPropertyList 2.2.8
    Using RedCloth 4.2.9
    Installing aasm 4.0.3
    Using i18n 0.7.0
    Using json 1.8.2
    Installing minitest 5.6.0
    Using thread_safe 0.3.5
    Using tzinfo 1.2.2
    Installing activesupport 4.2.0.rc3
    Using builder 3.2.2
    Using erubis 2.7.0
    Using mini_portile 0.6.2
    Using nokogiri 1.6.6.2
    Using rails-deprecated_sanitizer 1.0.3
    Installing rails-dom-testing 1.0.5
    Installing loofah 2.0.1
    Installing rails-html-sanitizer 1.0.1
    Installing actionview 4.2.0.rc3
    Installing rack 1.6.0.beta2
    Installing rack-test 0.6.2
    Installing actionpack 4.2.0.rc3
    Installing globalid 0.3.0
    Installing activejob 4.2.0.rc3
    Installing mime-types 2.4.3
    Using mail 2.6.3
    Installing actionmailer 4.2.0.rc3
    Installing actionpack-page_caching 1.0.2
    Installing activemerchant 1.48.0
    Installing activemodel 4.2.0.rc3
    Using arel 6.0.0
    Installing activerecord 4.2.0.rc3
    Installing addressable 2.3.6
    Installing afm 0.2.2
    Installing american_date 1.1.0
    Installing excon 0.41.0
    Installing formatador 0.2.5
    Installing net-ssh 2.9.1
    Installing net-scp 1.2.1
    Installing fog-core 1.25.0
    Installing multi_json 1.10.1
    Installing fog-json 1.0.0
    Installing inflecto 0.0.2
    Installing fog-brightbox 0.7.0
    Installing fog-xml 0.1.1
    Installing fog-profitbricks 0.0.1
    Installing fog-radosgw 0.0.3
    Installing fog-sakuracloud 0.1.1
    Installing fog-softlayer 0.3.24
    Installing fog-terremark 0.0.3
    Installing fission 0.5.0
    Installing fog-vmfusion 0.0.1
    Installing fog-voxel 0.0.1
    Installing ipaddress 0.8.0
    Installing trollop 2.0
    Installing rbvmomi 1.8.2
    Installing opennebula 4.10.1
    Installing fog 1.25.0
    Installing unf_ext 0.0.6
    Installing unf 0.1.4
    Installing asset_sync 1.1.0
    Installing request_store 1.1.0
    Installing ffi 1.9.6
    Installing ffi-compiler 0.1.3
    Installing scrypt 1.2.1
    Using authlogic 3.4.3 from git://github.com/drhenner/authlogic.git (at rails4.2)
    Installing autotest-rails-pure 4.1.2
    Installing awesome_nested_set 3.0.1
    Installing aws-sdk-v1 1.59.0
    Installing aws-sdk 1.59.0
    Installing coderay 1.1.0
    Installing better_errors 2.0.0
    Using debug_inspector 0.0.2
    Using binding_of_caller 0.7.2
    Installing bluecloth 2.2.0
    Installing columnize 0.8.9
    Installing debugger-linecache 1.2.0
    Installing slop 3.6.0
    Installing byebug 3.5.1
    Installing cancan 1.6.10
    Installing xpath 2.0.0
    Installing capybara 2.4.4
    Installing choice 0.1.6
    Installing chronic 0.10.2
    Installing chunky_png 1.3.3
    Installing climate_control 0.0.3
    Installing cocaine 0.5.4
    Installing sass 3.4.9
    Installing compass-core 1.0.1
    Installing compass-import-once 1.0.5
    Using rb-fsevent 0.9.4
    Using rb-inotify 0.9.5
    Installing compass 1.0.1
    Installing compass-rails 2.0.1
    Installing database_cleaner 1.3.0
    Installing diff-lcs 1.2.5
    Installing dynamic_form 1.1.4
    Installing launchy 2.4.3
    Installing email_spec 1.6.0
    Installing execjs 2.2.2
    Installing factory_girl 4.5.0
    Using thor 0.19.1
    Installing railties 4.2.0.rc3
    Installing factory_girl_rails 4.5.0
    Installing faker 1.4.3
    Installing friendly_id 5.1.0.beta.1
    Installing hashery 2.1.1
    Installing hike 1.2.3
    Installing jbuilder 2.2.5
    Installing jquery-rails 4.0.0
    Installing jquery-ui-rails 5.0.2
    Installing metaclass 0.0.4
    Installing mocha 0.13.3

    Gem::Ext::BuildError: ERROR: Failed to build gem native extension.

        /usr/bin/ruby2.2 -r ./siteconf20150510-2116-14qgpxa.rb extconf.rb
    checking for ruby/thread.h... yes
    checking for rb_thread_call_without_gvl() in ruby/thread.h... yes
    checking for rb_thread_blocking_region()... no
    checking for rb_wait_for_single_fd()... yes
    checking for rb_hash_dup()... yes
    checking for rb_intern3()... yes
    checking for mysql_query() in -lmysqlclient... no
    checking for main() in -lm... yes
    checking for mysql_query() in -lmysqlclient... no
    checking for main() in -lz... yes
    checking for mysql_query() in -lmysqlclient... no
    checking for main() in -lsocket... no
    checking for mysql_query() in -lmysqlclient... no
    checking for main() in -lnsl... yes
    checking for mysql_query() in -lmysqlclient... no
    checking for main() in -lmygcc... no
    checking for mysql_query() in -lmysqlclient... no
    *** extconf.rb failed ***
    Could not create Makefile due to some reason, probably lack of necessary
    libraries and/or headers.  Check the mkmf.log file for more details.  You may
    need configuration options.

    Provided configuration options:
    	--with-opt-dir
    	--without-opt-dir
    	--with-opt-include
    	--without-opt-include=${opt-dir}/include
    	--with-opt-lib
    	--without-opt-lib=${opt-dir}/lib
    	--with-make-prog
    	--without-make-prog
    	--srcdir=.
    	--curdir
    	--ruby=/usr/bin/$(RUBY_BASE_NAME)2.2
    	--with-mysql-dir
    	--without-mysql-dir
    	--with-mysql-include
    	--without-mysql-include=${mysql-dir}/include
    	--with-mysql-lib
    	--without-mysql-lib=${mysql-dir}/lib
    	--with-mysql-config
    	--without-mysql-config
    	--with-mysql-dir
    	--without-mysql-dir
    	--with-mysql-include
    	--without-mysql-include=${mysql-dir}/include
    	--with-mysql-lib
    	--without-mysql-lib=${mysql-dir}/lib
    	--with-mysqlclientlib
    	--without-mysqlclientlib
    	--with-mlib
    	--without-mlib
    	--with-mysqlclientlib
    	--without-mysqlclientlib
    	--with-zlib
    	--without-zlib
    	--with-mysqlclientlib
    	--without-mysqlclientlib
    	--with-socketlib
    	--without-socketlib
    	--with-mysqlclientlib
    	--without-mysqlclientlib
    	--with-nsllib
    	--without-nsllib
    	--with-mysqlclientlib
    	--without-mysqlclientlib
    	--with-mygcclib
    	--without-mygcclib
    	--with-mysqlclientlib
    	--without-mysqlclientlib

    extconf failed, exit code 1

    Gem files will remain installed in /tmp/bundler20150510-2116-1491i92/mysql2-0.3.17/gems/mysql2-0.3.17 for inspection.
    Results logged to /tmp/bundler20150510-2116-1491i92/mysql2-0.3.17/extensions/x86_64-linux/2.2.0/mysql2-0.3.17/gem_make.out
    An error occurred while installing mysql2 (0.3.17), and Bundler cannot continue.
    Make sure that `gem install mysql2 -v '0.3.17'` succeeds before bundling.

install mysql2:

    sudo gem install mysql2

result:安装失败。
安装依赖库：

    sudo apt-get install libmysqlclient-dev

再安装mysql2:

    sudo gem install mysql2

result:

    Building native extensions.  This could take a while...
    Successfully installed mysql2-0.3.18
    Parsing documentation for mysql2-0.3.18
    Installing ri documentation for mysql2-0.3.18
    Done installing documentation for mysql2 after 0 seconds
    1 gem installed

安装 rspec-support：

    Fetching: rspec-support-3.1.2.gem (100%)
    Successfully installed rspec-support-3.1.2
    Parsing documentation for rspec-support-3.1.2
    Installing ri documentation for rspec-support-3.1.2
    Done installing documentation for rspec-support after 0 seconds
    1 gem installed

运行 bundle install:

    Fetching gem metadata from http://rubygems.org/.............
    Fetching version metadata from http://rubygems.org/...
    Fetching dependency metadata from http://rubygems.org/..
    Using rake 10.4.2
    Using Ascii85 1.0.2
    Using CFPropertyList 2.2.8
    Using RedCloth 4.2.9
    Using aasm 4.0.3
    Using i18n 0.7.0
    Using json 1.8.2
    Using minitest 5.6.0
    Using thread_safe 0.3.5
    Using tzinfo 1.2.2
    Using activesupport 4.2.0.rc3
    Using builder 3.2.2
    Using erubis 2.7.0
    Using mini_portile 0.6.2
    Using nokogiri 1.6.6.2
    Using rails-deprecated_sanitizer 1.0.3
    Using rails-dom-testing 1.0.5
    Using loofah 2.0.1
    Using rails-html-sanitizer 1.0.1
    Using actionview 4.2.0.rc3
    Using rack 1.6.0.beta2
    Using rack-test 0.6.2
    Using actionpack 4.2.0.rc3
    Using globalid 0.3.0
    Using activejob 4.2.0.rc3
    Using mime-types 2.4.3
    Using mail 2.6.3
    Using actionmailer 4.2.0.rc3
    Using actionpack-page_caching 1.0.2
    Using activemerchant 1.48.0
    Using activemodel 4.2.0.rc3
    Using arel 6.0.0
    Using activerecord 4.2.0.rc3
    Using addressable 2.3.6
    Using afm 0.2.2
    Using american_date 1.1.0
    Using excon 0.41.0
    Using formatador 0.2.5
    Using net-ssh 2.9.1
    Using net-scp 1.2.1
    Using fog-core 1.25.0
    Using multi_json 1.10.1
    Using fog-json 1.0.0
    Using inflecto 0.0.2
    Using fog-brightbox 0.7.0
    Using fog-xml 0.1.1
    Using fog-profitbricks 0.0.1
    Using fog-radosgw 0.0.3
    Using fog-sakuracloud 0.1.1
    Using fog-softlayer 0.3.24
    Using fog-terremark 0.0.3
    Using fission 0.5.0
    Using fog-vmfusion 0.0.1
    Using fog-voxel 0.0.1
    Using ipaddress 0.8.0
    Using trollop 2.0
    Using rbvmomi 1.8.2
    Using opennebula 4.10.1
    Using fog 1.25.0
    Using unf_ext 0.0.6
    Using unf 0.1.4
    Using asset_sync 1.1.0
    Using request_store 1.1.0
    Using ffi 1.9.6
    Using ffi-compiler 0.1.3
    Using scrypt 1.2.1
    Using authlogic 3.4.3 from git://github.com/drhenner/authlogic.git (at rails4.2)
    Using autotest-rails-pure 4.1.2
    Using awesome_nested_set 3.0.1
    Using aws-sdk-v1 1.59.0
    Using aws-sdk 1.59.0
    Using coderay 1.1.0
    Using better_errors 2.0.0
    Using debug_inspector 0.0.2
    Using binding_of_caller 0.7.2
    Using bluecloth 2.2.0
    Using columnize 0.8.9
    Using debugger-linecache 1.2.0
    Using slop 3.6.0
    Using byebug 3.5.1
    Using cancan 1.6.10
    Using xpath 2.0.0
    Using capybara 2.4.4
    Using choice 0.1.6
    Using chronic 0.10.2
    Using chunky_png 1.3.3
    Using climate_control 0.0.3
    Using cocaine 0.5.4
    Using sass 3.4.9
    Using compass-core 1.0.1
    Using compass-import-once 1.0.5
    Using rb-fsevent 0.9.4
    Using rb-inotify 0.9.5
    Using compass 1.0.1
    Using compass-rails 2.0.1
    Using database_cleaner 1.3.0
    Using diff-lcs 1.2.5
    Using dynamic_form 1.1.4
    Using launchy 2.4.3
    Using email_spec 1.6.0
    Using execjs 2.2.2
    Using factory_girl 4.5.0
    Using thor 0.19.1
    Using railties 4.2.0.rc3
    Using factory_girl_rails 4.5.0
    Using faker 1.4.3
    Using friendly_id 5.1.0.beta.1
    Using hashery 2.1.1
    Using hike 1.2.3
    Using jbuilder 2.2.5
    Using jquery-rails 4.0.0
    Using jquery-ui-rails 5.0.2
    Using metaclass 0.0.4
    Using mocha 0.13.3
    Using paperclip 4.2.0
    Using ruby-rc4 0.1.5
    Using ttfunk 1.0.3
    Using pdf-reader 1.3.3
    Using prawn 0.12.0
    Using railroady 1.2.0
    Using bundler 1.9.6
    Using tilt 1.4.1
    Using sprockets 2.11.0
    Using sprockets-rails 2.0.1
    Using rails 4.2.0.rc3
    Using ruby-graphviz 1.0.9
    Using rails-erd 1.1.0
    Using rails3-generators 1.0.0
    Using rails_config 0.4.2
    Installing rmagick 2.13.3
    Using rspec-support 3.1.2
    Installing rspec-core 3.1.7
    Installing rspec-expectations 3.1.2
    Installing rspec-mocks 3.1.3
    Installing rspec-rails 3.1.0
    Installing rspec-rails-mocha 0.3.2
    Installing sass-rails 4.0.1
    Using sqlite3 1.3.10
    Installing uglifier 2.5.3
    Installing will_paginate 3.0.7
    Installing yard 0.8.7.6
    Installing zurb-foundation 4.3.2
    Bundle complete! 53 Gemfile dependencies, 142 gems now installed.
    Gems in the group production were not installed.
    Use `bundle show [gemname]` to see where a bundled gem is installed.
    Post-install message from rmagick:
    Please report any bugs. See https://github.com/gemhome/rmagick/compare/RMagick_2-13-2...master and https://github.com/rmagick/rmagick/issues/18


重新运行命令安装gems构建app:

    sudo gem install bundler

result:

    Fetching: bundler-1.9.7.gem (100%)
    Successfully installed bundler-1.9.7
    Parsing documentation for bundler-1.9.7
    Installing ri documentation for bundler-1.9.7
    Done installing documentation for bundler after 4 seconds
    1 gem installed

运行bundle install:

    bundle install

result:

    Using rake 10.4.2
    Using Ascii85 1.0.2
    Using CFPropertyList 2.2.8
    Using RedCloth 4.2.9
    Using aasm 4.0.3
    Using i18n 0.7.0
    Using json 1.8.2
    Using minitest 5.6.0
    Using thread_safe 0.3.5
    Using tzinfo 1.2.2
    Using activesupport 4.2.0.rc3
    Using builder 3.2.2
    Using erubis 2.7.0
    Using mini_portile 0.6.2
    Using nokogiri 1.6.6.2
    Using rails-deprecated_sanitizer 1.0.3
    Using rails-dom-testing 1.0.5
    Using loofah 2.0.1
    Using rails-html-sanitizer 1.0.1
    Using actionview 4.2.0.rc3
    Using rack 1.6.0.beta2
    Using rack-test 0.6.2
    Using actionpack 4.2.0.rc3
    Using globalid 0.3.0
    Using activejob 4.2.0.rc3
    Using mime-types 2.4.3
    Using mail 2.6.3
    Using actionmailer 4.2.0.rc3
    Using actionpack-page_caching 1.0.2
    Using activemerchant 1.48.0
    Using activemodel 4.2.0.rc3
    Using arel 6.0.0
    Using activerecord 4.2.0.rc3
    Using addressable 2.3.6
    Using afm 0.2.2
    Using american_date 1.1.0
    Using excon 0.41.0
    Using formatador 0.2.5
    Using net-ssh 2.9.1
    Using net-scp 1.2.1
    Using fog-core 1.25.0
    Using multi_json 1.10.1
    Using fog-json 1.0.0
    Using inflecto 0.0.2
    Using fog-brightbox 0.7.0
    Using fog-xml 0.1.1
    Using fog-profitbricks 0.0.1
    Using fog-radosgw 0.0.3
    Using fog-sakuracloud 0.1.1
    Using fog-softlayer 0.3.24
    Using fog-terremark 0.0.3
    Using fission 0.5.0
    Using fog-vmfusion 0.0.1
    Using fog-voxel 0.0.1
    Using ipaddress 0.8.0
    Using trollop 2.0
    Using rbvmomi 1.8.2
    Using opennebula 4.10.1
    Using fog 1.25.0
    Using unf_ext 0.0.6
    Using unf 0.1.4
    Using asset_sync 1.1.0
    Using request_store 1.1.0
    Using ffi 1.9.6
    Using ffi-compiler 0.1.3
    Using scrypt 1.2.1
    Using authlogic 3.4.3 from git://github.com/drhenner/authlogic.git (at rails4.2)
    Using autotest-rails-pure 4.1.2
    Using awesome_nested_set 3.0.1
    Using aws-sdk-v1 1.59.0
    Using aws-sdk 1.59.0
    Using coderay 1.1.0
    Using better_errors 2.0.0
    Using debug_inspector 0.0.2
    Using binding_of_caller 0.7.2
    Using bluecloth 2.2.0
    Using columnize 0.8.9
    Using debugger-linecache 1.2.0
    Using slop 3.6.0
    Using byebug 3.5.1
    Using cancan 1.6.10
    Using xpath 2.0.0
    Using capybara 2.4.4
    Using choice 0.1.6
    Using chronic 0.10.2
    Using chunky_png 1.3.3
    Using climate_control 0.0.3
    Using cocaine 0.5.4
    Using sass 3.4.9
    Using compass-core 1.0.1
    Using compass-import-once 1.0.5
    Using rb-fsevent 0.9.4
    Using rb-inotify 0.9.5
    Using compass 1.0.1
    Using compass-rails 2.0.1
    Using database_cleaner 1.3.0
    Using diff-lcs 1.2.5
    Using dynamic_form 1.1.4
    Using launchy 2.4.3
    Using email_spec 1.6.0
    Using execjs 2.2.2
    Using factory_girl 4.5.0
    Using thor 0.19.1
    Using railties 4.2.0.rc3
    Using factory_girl_rails 4.5.0
    Using faker 1.4.3
    Using friendly_id 5.1.0.beta.1
    Using hashery 2.1.1
    Using hike 1.2.3
    Using jbuilder 2.2.5
    Using jquery-rails 4.0.0
    Using jquery-ui-rails 5.0.2
    Using metaclass 0.0.4
    Using mocha 0.13.3
    Using paperclip 4.2.0
    Using ruby-rc4 0.1.5
    Using ttfunk 1.0.3
    Using pdf-reader 1.3.3
    Using prawn 0.12.0
    Using railroady 1.2.0
    Using bundler 1.9.7
    Using tilt 1.4.1
    Using sprockets 2.11.0
    Using sprockets-rails 2.0.1
    Using rails 4.2.0.rc3
    Using ruby-graphviz 1.0.9
    Using rails-erd 1.1.0
    Using rails3-generators 1.0.0
    Using rails_config 0.4.2
    Using rmagick 2.13.3
    Using rspec-support 3.1.2
    Using rspec-core 3.1.7
    Using rspec-expectations 3.1.2
    Using rspec-mocks 3.1.3
    Using rspec-rails 3.1.0
    Using rspec-rails-mocha 0.3.2
    Using sass-rails 4.0.1
    Using sqlite3 1.3.10
    Using uglifier 2.5.3
    Using will_paginate 3.0.7
    Using yard 0.8.7.6
    Using zurb-foundation 4.3.2
    Bundle complete! 53 Gemfile dependencies, 142 gems now installed.
    Gems in the group production were not installed.
    Use `bundle show [gemname]` to see where a bundled gem is installed.

运行命令：rake db:create:all

    rake db:create:all

resu:

    /var/lib/gems/2.2.0/gems/fog-core-1.25.0/lib/fog/core/collection.rb:144: warning: circular argument reference - filters
    /var/lib/gems/2.2.0/gems/compass-core-1.0.1/lib/compass/core/caniuse.rb:72: warning: circular argument reference - browsers

运行rake db:migrate db:seed

    rake db:migrate db:seed

result:

    ......
    == 20100814070158 CreateVariantSuppliers: migrating ===========================
    -- create_table(:variant_suppliers)
       -> 0.0044s
    -- add_index(:variant_suppliers, :variant_id)
       -> 0.0017s
    -- add_index(:variant_suppliers, :supplier_id)
       -> 0.0034s
    == 20100814070158 CreateVariantSuppliers: migrated (0.0099s) ==================

    == 20100814070240 CreateBrands: migrating =====================================
    -- create_table(:brands)
       -> 0.0018s
    == 20100814070240 CreateBrands: migrated (0.0020s) ============================
    ......
    == 20130719071644 RemoveBirthDateFromUsers: migrating =========================
    -- remove_column(:users, :birth_date)
       -> 0.0597s
    == 20130719071644 RemoveBirthDateFromUsers: migrated (0.0599s) ================

    == 20131123212228 MoveBrandToProducts: migrating ==============================
    -- remove_column(:variants, :brand_id)
       -> 0.0401s
    == 20131123212228 MoveBrandToProducts: migrated (0.0403s) =====================

    START SEEDING
    COUNTRIES
    States
    ROLES
    Address Types
    PHONE TYPES
    Item Types
    DEAL TYPES
    Accounts
    SHIPPING RATE TYPES
    Shipping Zones
    ACCOUNT TYPES
    Return Reasons
    Return CONDITIONS
    Newsletters
    Referral Bonuses
    Referral PROGRAMS

运行 rake db:test:prepare:

    /var/lib/gems/2.2.0/gems/fog-core-1.25.0/lib/fog/core/collection.rb:144: warning: circular argument reference - filters
    /var/lib/gems/2.2.0/gems/compass-core-1.0.1/lib/compass/core/caniuse.rb:72: warning: circular argument reference - browsers

    ************************************************
         It is Recommended to use dalli_store.  go to config/initializers/session_store.rb for details
    ************************************************

          ############################################################################################
          ############################################################################################
          !  You need to setup the settings.yml
          !  copy settings.yml.example to settings.yml
          !
          !  YOUR ENV variables are not ready for checkout!
          !  please adjust ENV['AUTHNET_LOGIN'] && ENV['AUTHNET_PASSWORD']
          !  if you are not using authorize.net go to each file in /config/environments/*.rb and
          !  adjust the following code accordingly...

          ::GATEWAY = ActiveMerchant::Billing::AuthorizeNetGateway.new(
            :login    => Settings.authnet.login,
            :password => Settings.authnet.password
          )

          !  This is required for the checkout process to work.
          !
          !  Remove or Adjust this warning in /config/environment.rb for developers on your team
          !  once you everything working with your specific Gateway.
          ############################################################################################

    START SEEDING
    COUNTRIES
    States
    ROLES
    Address Types
    PHONE TYPES
    Item Types
    DEAL TYPES
    Accounts
    SHIPPING RATE TYPES
    Shipping Zones
    ACCOUNT TYPES
    Return Reasons
    Return CONDITIONS
    Newsletters
    Referral Bonuses
    Referral PROGRAMS

运行rails server:

    rails server

打开浏览器：http://localhost:3000

<img src='/images/rails_localhost.png' />

出现一大堆错误。上网寻找解决方案，安装缺失的组件，重新安装并构建，运行

<img src='/images/ruby_on_rails.png' />

