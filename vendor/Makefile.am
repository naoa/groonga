# Copyright(C) 2017 Brazil
# Copyright(C) 2019 Sutou Kouhei <kou@clear-code.com>
#
# This library is free software; you can redistribute it and/or
# modify it under the terms of the GNU Lesser General Public
# License version 2.1 as published by the Free Software Foundation.
#
# This library is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
# Lesser General Public License for more details.
#
# You should have received a copy of the GNU Lesser General Public
# License along with this library; if not, write to the Free Software
# Foundation, Inc., 51 Franklin Street, Fifth Floor, Boston, MA  02110-1301  USA

NGINX_DIR = nginx-$(NGINX_VERSION)

SUBDIRS =					\
	lz4					\
	onigmo					\
	mecab					\
	message_pack				\
	mruby					\
	groonga-log				\
	rapidjson

EXTRA_DIST =					\
	$(NGINX_DIR)				\
	CMakeLists.txt				\
	plugins/CMakeLists.txt			\
	download_groonga_normalizer_mysql.rb	\
	download_lz4.rb				\
	download_mecab.rb			\
	download_message_pack.rb		\
	download_rapidjson.rb

dist-hook:
	rm -rf $(distdir)/$(NGINX_DIR)/objs/
	GIT_DIR=$(srcdir)/mruby-source/.git git archive --format=tar HEAD | \
	  tar xf - -C $(distdir)/mruby-source
	$(MKDIR_P) $(distdir)/onigmo-source
	GIT_DIR=$(srcdir)/onigmo-source/.git git archive --format=tar HEAD | \
	  tar xf - -C $(distdir)/onigmo-source
	cd $(distdir)/onigmo-source && autoreconf --install --force
	cd $(distdir)/onigmo-source && sleep 1 && touch config.h.in
	$(MKDIR_P) $(distdir)/ngx_mruby-source
	GIT_DIR=$(srcdir)/ngx_mruby-source/.git git archive --format=tar HEAD | \
	  tar xf - -C $(distdir)/ngx_mruby-source
	$(MKDIR_P) $(distdir)/groonga-log-source
	GIT_DIR=$(srcdir)/groonga-log-source/.git git archive --format=tar HEAD | \
	  tar xf - -C $(distdir)/groonga-log-source
	cd $(distdir) && $(RUBY) download_rapidjson.rb
