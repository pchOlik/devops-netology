#1) Найдите полный хеш и комментарий коммита, хеш которого начинается на aefea.

$ git show aefea
commit aefead2207ef7e2aa5dc81a34aedf0cad4c32545
Author: Alisdair McDiarmid <alisdair@users.noreply.github.com>
Date:   Thu Jun 18 10:29:58 2020 -0400

    Update CHANGELOG.md

diff --git a/CHANGELOG.md b/CHANGELOG.md
index 86d70e3e0d..588d807b17 100644
--- a/CHANGELOG.md
+++ b/CHANGELOG.md


#2) Какому тегу соответствует коммит 85024d3?


$ git show 85024d3
commit 85024d3100126de36331c6982bfaac02cdab9e76 (tag: v0.12.23)
Author: tf-release-bot <terraform@hashicorp.com>
Date:   Thu Mar 5 20:56:10 2020 +0000

    v0.12.23


#3) Сколько родителей у коммита b8d720? Напишите их хеши.


*   b8d720f834 Merge pull request #23916 from hashicorp/cgriggs01-stable
|\
| * 9ea88f22fc add/update community provider listings
|/
*   56cd7859e0 Merge pull request #23857 from hashicorp/cgriggs01-stable

$ git show b8d720^1
commit 56cd7859e05c36c06b56d013b55a252d0bb7e158

$ git show b8d720^2
commit 9ea88f22fc6269854151c571162c5bcf958bee2b


#4)Перечислите хеши и комментарии всех коммитов которые были сделаны между тегами v0.12.23 и v0.12.24.

$ git log v0.12.22..v0.12.24 --pretty=oneline
33ff1c03bb960b332be3af2e333462dde88b279e (tag: v0.12.24) v0.12.24
b14b74c4939dcab573326f4e3ee2a62e23e12f89 [Website] vmc provider links
3f235065b9347a758efadc92295b540ee0a5e26e Update CHANGELOG.md
6ae64e247b332925b872447e9ce869657281c2bf registry: Fix panic when server is unreachable
5c619ca1baf2e21a155fcdb4c264cc9e24a2a353 website: Remove links to the getting started guide's old location
06275647e2b53d97d4f0a19a0fec11f6d69820b5 Update CHANGELOG.md
d5f9411f5108260320064349b757f55c09bc4b80 command: Fix bug when using terraform login on Windows
4b6d06cc5dcb78af637bbb19c198faff37a066ed Update CHANGELOG.md
dd01a35078f040ca984cdd349f18d0b67e486c35 Update CHANGELOG.md
225466bc3e5f35baa5d07197bbc079345b77525e Cleanup after v0.12.23 release
85024d3100126de36331c6982bfaac02cdab9e76 (tag: v0.12.23) v0.12.23
4703cb6c1c7a00137142da867588a5752c54fa6a Update CHANGELOG.md
0b4470e0d45b2818f385eee5daf0816838de84ef Cleanup after v0.12.22 release


#5) Найдите коммит в котором была создана функция func providerSource, ее определение в коде выглядит так func providerSource(...) (вместо троеточия перечислены аргументы).



$ git log -S "func providerSource" --pretty=format:'%ad %h %s'
Tue Apr 21 16:28:59 2020 -0700 5af1e6234a main: Honor explicit provider_installation CLI config when present

Thu Apr 2 18:04:39 2020 -0700 8c928e8358 main: Consult local directories as potential mirrors of providers


#6) Найдите все коммиты в которых была изменена функция globalPluginDirs.

$ git grep globalPluginDirs
commands.go:            GlobalPluginDirs: globalPluginDirs(),
commands.go:    helperPlugins := pluginDiscovery.FindPlugins("credentials", globalPluginDirs())
internal/command/cliconfig/config_unix.go:              // FIXME: homeDir gets called from globalPluginDirs during init, before
plugins.go:// globalPluginDirs returns directories that should be searched for
plugins.go:func globalPluginDirs() []string {



$ git log -L :globalPluginDirs:commands.go
fatal: -L parameter 'globalPluginDirs' starting at line 1: no match

$ git log -L :globalPluginDirs:./internal/command/cliconfig/config_unix.go
fatal: -L parameter 'globalPluginDirs' starting at line 1: no match

$ git log -L :globalPluginDirs:plugins.go
commit 78b12205587fe839f10d946ea3fdc06719decb05
Author: Pam Selle <204372+pselle@users.noreply.github.com>
Date:   Mon Jan 13 16:50:05 2020 -0500
...........
52dbf94834cb970b510f2fba853a5b49ad9b1a46 keep .terraform.d/plugins for discover
...........
41ab0aef7a0fe030e84018973a64135b11abcd70 Add missing OS_ARCH dir to global plugin paths
...........
66ebff90cdfaa6938f26f908c7ebad8d547fea17 move some more plugin search path logic to command
..........
8364383c359a6b738a436d1b7745ccdce178df47 Push plugin discovery down into command package


#7)Кто автор функции synchronizedWriters? - Martin Atkins

$ git log -S 'synchronizedWrite' --pretty=format:'%ad %an %s'

Mon Nov 30 18:02:04 2020 -0500 James Bardin remove unused
Wed Oct 21 13:06:23 2020 -0400 James Bardin remove prefixed io
Wed May 3 16:25:41 2017 -0700 Martin Atkins main: synchronize writes to VT100-faker on Windows



