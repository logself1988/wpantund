#
# Copyright (c) 2016 Nest Labs, Inc.
# All rights reserved.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#    http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#

AM_CPPFLAGS = \
	-I$(top_srcdir)/src \
	-I$(top_srcdir)/src/util \
	-I$(top_srcdir)/src/ipc-dbus \
	-I$(top_srcdir)/third_party/fgetln \
	-I$(top_srcdir)/third_party/pt \
	-I$(top_srcdir)/third_party/assert-macros \
	$(NULL)

DISTCLEANFILES = \
	.deps \
	Makefile \
	$(NULL)

EXTRA_DIST = \
	wpantund.conf \
	$(NULL)

pkginclude_HEADERS = \
	wpan-properties.h \
	wpan-error.h \
	$(NULL)

sysconf_DATA = wpantund.conf

sbin_PROGRAMS = wpantund

wpantund_SOURCES = \
	wpantund.cpp \
	wpantund.h \
	IPCServer.h \
	NCPConstants.h \
	NCPControlInterface.cpp \
	NCPControlInterface.h \
	NCPInstance.cpp \
	NCPInstance.h \
	NCPInstanceBase.cpp \
	NCPInstanceBase.h \
	NCPMfgInterface_v0.h \
	NCPMfgInterface_v1.h \
	NetworkInstance.h \
	NCPConstants.h \
	FirmwareUpgrade.h \
	FirmwareUpgrade.cpp \
	StatCollector.h \
	StatCollector.cpp \
	RunawayResetBackoffManager.cpp \
	RunawayResetBackoffManager.h \
	NCPInstanceBase-NetInterface.cpp \
	NCPInstanceBase-Addresses.cpp \
	NCPInstanceBase-AsyncIO.cpp \
	NCPTypes.h \
	NCPTypes.cpp \
	NetworkRetain.h \
	NetworkRetain.cpp \
	../util/IPv6PacketMatcher.cpp \
	../util/IPv6Helpers.cpp \
	../util/tunnel.c \
	../util/config-file.c \
	../util/socket-utils.c \
	../util/any-to.cpp \
	../util/string-utils.c \
	../util/time-utils.c \
	../util/nlpt-select.c \
	../util/Data.cpp \
	../util/SocketWrapper.cpp \
	../util/SocketAdapter.cpp \
	../util/UnixSocket.cpp \
	../util/SuperSocket.cpp \
	../util/EventHandler.cpp \
	../util/TunnelIPv6Interface.cpp \
	../util/ValueMap.cpp \
	../util/Timer.cpp \
	../util/sec-random.c \
	$(NULL)

wpantund_LDADD =  $(DBUS_LIBS)
wpantund_LDADD += ../ipc-dbus/libwpantund-dbus.la

if STATIC_LINK_NCP_PLUGIN
wpantund_LDADD += ../ncp-@default_ncp_plugin@/libncp-@default_ncp_plugin@.la
else
wpantund_LDADD += $(LIBDL_LIBS)
wpantund_LDFLAGS = @EXPORT_DYNAMIC_LDFLAGS@
endif

wpantund_CPPFLAGS = $(AM_CPPFLAGS) $(DBUS_CFLAGS)
wpantund_CXXFLAGS = $(BOOST_CXXFLAGS)

SOURCE_VERSION=$(shell                                            \
	git describe --dirty --always --match "[0-9].*" 2> /dev/null  \
)

BUILT_SOURCES  = $(top_builddir)/$(subdir)/version.c
CLEANFILES     = $(top_builddir)/$(subdir)/version.c
.INTERMEDIATE:   $(top_builddir)/$(subdir)/version.c wpantund-version.$(OBJEXT)

$(top_builddir)/$(subdir)/version.c: ../version.c.in Makefile
	sed 's/SOURCE_VERSION/"$(SOURCE_VERSION)"/' < $< > $@

wpantund_SOURCES += $(top_builddir)/$(subdir)/version.c
